---
layout: post
title:  "Reading about gas fermentation and the engineering of anaerobic organisms"
date:   2023-02-02 12:00:00 -0500
categories: jekyll update
---
In this post I'll review my recent reading of two very interesting articles:
- Cell-free prototyping enables implementation of optimized reverse beta-oxidation pathways in heterotrophic and autotrophic bactera by Vogeli et al. [Link][vogeli-2022]
- Stepping on the gas to a circular economy: Accelerating development of caron-negative chemical production from gas fermentation by Fackler et al. [Link][fackler-2021]

# Cell-free prototyping
The authors in this article present the development of an engineering pipeline that allows to test biochemical pathways *in vitro* for the selective production of several chemicals. After testing the pathways are implemented *in vivo* and validated. 

The article focuses on the reverse beta-oxidation pathway (r-BOX). This is a circular metabolic pathway that has the potential to produce hundreds of different molecules. In contrast, linear pathways limit the co-development of multiple biochemical products. One of the goals of the engineering procedure is to increase the selectivity of r-BOX to focus on certain chemicals. The authors achieve this by using [iPROBE][iprobe], a cell-free pipeline for testing combination of enzymes. In a nutshell, iPROBE entails expressing proteins in a TX-TL reaction, providing substrates, and then quantifying the desired output. 

Reactions are scaled down to 4 uL and carried out in 96-well plates which allows the researchers to automate most of the pipeline. Before any combinatorial pathway exploration takes place, the authors search for the best bacterial strain tomake the cell-free extract, test different core enzyme combinations, and optimize reaction conditions (pH, %fresh extract, CoA, NAD). Pathway exploration is performed in a pairwise manner and the best combination of enzymes is found *in vitro*. 

The best enzyme combination is selected for scale-up and shows a good correlation with what was observed *in vitro*. Importantly, the enzyme combination works in *E. coli* and *C. autoethanogenum* speaking to the versatility of this approach. 

## Outstanding questions
- How easily can this process be scaled up to test more enzyme combinations?
- Can the data be used in an AI/ML framework to predict the behavior of untested enzyme combinations?
- Can the process be adapted to microfluidics to test more combinations?

## Further reading
- [Pollution to products: Recycling of 'above ground' carbon by gas fermentation][kopke-2021]
- [In vitro prototyping and rapid optimization of biosynthetic enzymes for cell design][iprobe]
- [Modular cell-free expression plasmids to accelerate biological design in cells][karim-2020]



[vogeli-2022]: https://www.nature.com/articles/s41467-022-30571-6
[fackler-2021]: https://www.osti.gov/biblio/1807218
[iprobe]: https://www.nature.com/articles/s41589-020-0559-0
[kopke-2021]: https://doi.org/10.1016/j.copbio.2020.02.017 
[karim-2020]: https://doi.org/10.1093/synbio/ysaa019
