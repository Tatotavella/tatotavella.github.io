---
layout: post
title:  "Removing repetitive patterns in microscopy data using a Fourier filtering technique"
date:   2023-02-09 12:00:00 -0500
categories: jekyll update
---
One of my labmates works with cells on microposts. These microposts generate a repetitive background pattern in his microscopy images which complicates cell segmentation and tracking. I developed a simple pipeline to remove as much background as possible from his images. This post goes over how to do that.

Here's an example image from his dataset

![Example image with pattern in the background](/assets/images/2023-02-09-example-image.jpg)

you can see the little blobs which are the cells and the lines are the microposts in a regular array. The goal would be to have a smooth background and just the cells.

The main idea of the process is to do a Fourier transform of the image, remove the frequencies associated with the pattern, and do an inverse transform to obtain the filtered image. Because this is a timelapse dataset, we have a stack full of images over time. Thus, the first step is to get an average Fourier spectrum for that stack. I simply calculate the transform for each image and then average all of them together. The result is the following:

![Average Fourier transform](/assets/images/2023-02-09-fourier-transform.jpg)

> Side note: When you do an FFT of an image you get back a special type of data which has complex numbers for each pixel. However, when you do the average, you get an 8-bit image. This 8-bit image can't be used to do an inverse transform. Therefore, this average image is simply used to select which areas have the peaks and then for each frame we remove those areas from FFT's result (which is a complex number image).

Then, we select those regions that have a peak of intensity. These correspond to the background pattern.

![Peak selection in Fourier transform](/assets/images/2023-02-09-fourier-peak-selection.jpg)

and after selection we clear them out from the image


![Cleared Fourier transform](/assets/images/2023-02-09-cleared-peaks.jpg)

In this example I'm showing how the average FFT looks cleared. In the processing this isn't happening but rather, the individual FFT for each frame has these same sections removed.

> Side note: Notice that I just selected the top peaks, because of the symmetry of the transform, the result will have both top and bottom peaks removed. You can double-check this by doing FFT on the final result.

So finally, if we do an inverse FFT we get the desired result

![Final result](/assets/images/2023-02-09-result.jpg)


## Automating the process with ImageJ macros
Here's the code that I wrote to automate the process. The user is asked to select all the ROI's for the peaks and then the macro removes those from all images.

{% highlight java %}
// Open stack of BF images
file_path="C:/Users/tavel/Desktop/Experiments/Chun-Yen-Fourier-Filter/BF_only.tif"
open(file_path);
run("Enhance Contrast", "saturated=0.35");
rename("BF");

// Get average Fourier Transform of the stack
setBatchMode(true);
stack = getImageID;
n = nSlices;
for (i=1; i<=n; i++) {
   selectImage(stack);
   setSlice(i);
   run("FFT"); 
}
run("Images to Stack", "name=[FFT Stack] title=FFT");
setBatchMode(false);
run("Z Project...", "projection=[Average Intensity]");
close("FFT Stack");
selectWindow("AVG_FFT Stack");
rename("AVG_FFT");
run("Enhance Contrast", "saturated=0.35");

// Ask user to select ROIs on the upper part of the spectrum
roiManager("Reset");
waitForUser("ROI selection in spectrum", "Please select the peaks of the spectrum on the upper half of AVF_FFT. Add all selections to the ROI Manager. When finished click OK in this dialogue.");
n=roiManager("Count");
roiManager("Select", Array.getSequence(n));
roiManager("Combine");
roiManager("Add");
roiManager("Select",n);
close("AVG_FFT");

// Process each image
selectWindow("BF");
setBatchMode(true);
stack = getImageID;
n = nSlices;
for (i=1; i<=n; i++) {
   selectImage(stack);
   setSlice(i);
   run("FFT");
   rename("FFT");
   run("Restore Selection");
   run("Clear", "slice");
   run("Inverse FFT");
   close("FFT");
}
run("Images to Stack", "name=[Filtered] title=FFT");
setBatchMode(false);
run("Enhance Contrast", "saturated=0.35");
{% endhighlight %}
