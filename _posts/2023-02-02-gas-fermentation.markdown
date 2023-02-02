---
layout: post
title:  "Reading about gas fermentation and the engineering of anaerobic organisms"
date:   2023-02-02 12:00:00 -0500
categories: jekyll update
---
In this post I'll review my recent reading of two very interesting articles:
- Cell-free prototyping enables implementation of optimized reverse beta-oxidation pathways in heterotrophic and autotrophic bactera by Vogeli et al. [Link][vogeli-2022]
- Stepping on the gas to a circular economy: Accelerating development of caron-negative chemical production from gas fermentation by Fackler et al. [Link][fackler-2021]

## Cell-free prototyping
The authors in this article present the development of an engineering pipeline that allows to test biochemical pathways *in vitro* for the selective production of several chemicals. After testing the pathways are implemented *in vivo* and validated. 

The article focuses on the reverse beta-oxidation pathway (r-BOX). This is a circular metabolic pathway that has the potential to produce hundreds of different molecules. In contrast, linear pathways limit the co-development of multiple biochemical products. One of the goals of the engineering procedure is to increase the selectivity of r-BOX to focus on certain chemicals. The authors achieve this by using [iPROBE][iprobe], a cell-free pipeline for testing combination of enzymes. In a nutshell, iPROBE entails expressing proteins in a TX-TL reaction, providing substrates, and then quantifying the desired output. 

Reactions are scaled down to 4 uL and carried out in 96-well plates which allows the researchers to automate most of the pipeline. Before any combinatorial pathway exploration takes place, the authors search for the best bacterial strain tomake the cell-free extract, test different core enzyme combinations, and optimize reaction conditions (pH, %fresh extract, CoA, NAD). Pathway exploration is performed in a pairwise manner and the best combination of enzymes is found *in vitro*. 

The best enzyme combination is selected for scale-up and shows a good correlation with what was observed *in vitro*. Importantly, the enzyme combination works in *E. coli* and *C. autoethanogenum* speaking to the versatility of this approach. 

# Outstanding questions
- How easily can this process be scaled up to test more enzyme combinations?
- Can the data be used in an AI/ML framework to predict the behavior of untested enzyme combinations?
- Can the process be adapted to microfluidics to test more combinations?

# Further reading
- [Pollution to products: Recycling of 'above ground' carbon by gas fermentation][kopke-2021]
- [In vitro prototyping and rapid optimization of biosynthetic enzymes for cell design][iprobe]
- [Modular cell-free expression plasmids to accelerate biological design in cells][karim-2020]


## Gas fermentation Review
The second article is a very extensive review about the current state of gas fermentation. Gas fermentation is a very valuable tool in the fight against climate change. Despite the conversion that is happening in many industries from fossil fuel to renewables, there are many sectors that will remain heavily dependent on fossil resources for the foreseeable future, such as aviation fuel and chemical production. Therefore, there is a need for innovation in those sectors and gas fermentation provides a solution.

Typical fermentation depends heavily on agricultural feedstocks which have two main disadvantages. First, they are a source of food, so fermentation is effectively competing for this resource. Second, its availability fluctuates considerably, rendering its price and composition difficult to predict. Gas fermentation uses industrial off gases or syngas as the feedstock and does not suffer from the same problems that agricultural feedstocks have.

The main microorganisms used in gas fermentation are acetogenic bacteria. These bacteria contain the Wood-Ljungdahl Pathway (WLP) that fixates carbon anaerobically. It's considered to be the first biochemical pathway on Earth. Importantly, none of the WLP enzymes are membrane associated, with no cytochromes or quinones present.

Within the bioreactor these organisms actively convert CO, CO2, and H2 into useful chemicals. Typically, the gas fermentation process is run continuously, and due to the robustness of the organisms used, it can accept a varied composition of syngas as feedstock.

There are various applications for this type of fermentation. The most successful product so far is ethanol which can be used to blend with gasoline. Additionally, this ethanol can be used as a building block for more complex chemicals. Ethylene oxide and ethylene glycol can be used in the production of PET, the world's most used thermoplastic.

In terms of the tools available to engineer acetogens (being *Clostridium autoethanogenum* the most famous one), there has been a lot of development in the recent years. Genes can be inserted using either conjugation or electroporation and several genetic parts have been developed. Researchers are exploring the use of CRISPR tools on these organisms as well as cell-free prototyping tools to accelerate DBTL cycles. Finally, there are several system's biology tools that integrate genomic information with multi-omics data and metabolic modeling. An exciting area of development is the fluorescent reporter field. Typical reporters need oxygen to function so it's challenging to build reporters that work on anaerobic organisms. All in all gas fermentation using acetogens appears as a very valuable tool in the fight against climate change.

Recently, a cell-free platform was established for *C. autoethanogenum* that can produce up to 320 ug of protein per ml in semi-continuous tx-tl reactions. This allows to screen genetic parts on the native environment of *C. atuoethanogenum*. I really enjoyed the following passage from the paper:
> Together, cell-free systems from *E. coli* and nonmodel organisms will expedite engineering efforts in gas-fermenting microbes by increasing the throughput of genetic part characterization and accelerating development cycles for metabolic pathway optimization to more efficiently produce industrial strains that convert waste gas to chemical products

# Further reading
- [Redox controls metabolic robustness in the gas-fermenting acetogen *Clostridium autoethanogenum*][mahamkali-2020]
- [Syngas fermentation to alcohols: reactor technology and application perspective][stoll-2020]
- [A strongly fluorescing anaerobic reporter and protein-tagging system for *Clostridium* organisms][streett-2019]
- [Development of a clostridia-based cell-free system for prototyping genetic parts and metabolic pathways][kruger-2020]
- [Kinetic ensemble model of gas-fermenting *Clostridium autoethanogenum* for improved ethanol production][greene-2019]



[vogeli-2022]: https://www.nature.com/articles/s41467-022-30571-6
[fackler-2021]: https://www.osti.gov/biblio/1807218
[iprobe]: https://www.nature.com/articles/s41589-020-0559-0
[kopke-2021]: https://doi.org/10.1016/j.copbio.2020.02.017 
[karim-2020]: https://doi.org/10.1093/synbio/ysaa019
[mahamkali-2020]: https://www.pnas.org/doi/10.1073/pnas.1919531117
[stoll-2020]: https://doi.org/10.1002/cite.201900118
[streett-2019]: https://doi.org/10.1128/AEM.00622-19 
[kruger-2020]: https://doi.org/10.1016/j.ymben.2020.06.004
[greene-2019]: https://doi.org/10.1016/j.bej.2019.04.021

