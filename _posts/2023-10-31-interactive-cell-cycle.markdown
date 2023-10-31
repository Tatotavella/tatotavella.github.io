---
layout: post
title:  "Creating an interactive cell cycle simulation using ObservableHQ"
date:   2023-10-30 09:11:00 -0500
categories: jekyll update
---
In the [Yang lab](https://www-personal.umich.edu/~qiongy/), we usually work with ordinary differential equation models. These models help us guide our intuition. However, it's not straightforward to run a simulation every time we have a question about
the effect of a certain parameter on the output. That's why I built an [interactive simulation using Plotly-dash](https://github.com/YangLab-um/interactive-cell-cycle). This simulation works but it has several downsides. First, it's not easy to integrate
on existing websites because the free version of Plotly-dash makes it hard to do. Despite this, hosted the code on a free server and achieved a minimal working example of the app. Second, every time we change
a parameter, the simulation takes several seconds to finish. This is probably related to all the overhead of calling the server, running the simulation, and re-rendering the plots. 

Therefore, we decided to move on to ObservableHQ to create an app that's native to the web and that will be more responsive. Here's the final result:
<iframe width="100%" height="957" frameborder="0"
  src="https://observablehq.com/embed/3ad2343ac1f69afb@1197?cells=parameterSliders%2CrenderedPlots%2ChtmlStyling"></iframe>
