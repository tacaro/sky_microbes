# Microbes in the Skies

Microorganisms (bacteria, fungi, oomycota, etc.) are ubiquitous in the Earth's biosphere and influence global biogeochemical cycles, plant and animal disease, and possibly weather formation. The density and distribution of microorganisms in the atmosphere has been a recent focus of environmental microbiology research. To attempt to measure the diversity, quantity, and distribution of bacteria in the Earth's atmosphere, a C20-A jet, outfitted with an aerosol sampling instrument, was flown in the troposphere (0-10km) and lower stratosphere (12km)for the purpose of capturing microorganisms at altitude (Smith et al. 2018) https://doi.org/10.3389/fmicb.2018.01752.

Captured particulates on filters were DNA-extracted and sequenced with 16S amplicon sequencing. We used DADA2 (https://benjjneb.github.io/dada2/) to filter, denoise, and assign taxonomy to sequences. From the resulting amplicon sequence variants (ASVs)
We had 3 questions:
1. How does bacterial diversity change with altitude?
2. Are certain bacterial traits more common at high altitude?
3. How do individual bacteria genus/species quantities change with altitude?
For a more in-depth discussion of our results, see: https://docs.google.com/presentation/d/1sCioE0USSKTHt_sz-OolLQsAwSAc148L8Q9tcH-49LI/edit?usp=sharing

# BacDive Phenotype Analysis
To query the BacDive (http://bacdive.dsmz.de/) database for each of our ~4600 ASVs, we accessed the BacDive RESTful API with assistance from the BacDiveR package (https://github.com/TIBHannover/BacDiveR). For each ASV, we queried the BacDive database using a taxa name (Genus + Species when available, or just Genus). Two phenotypes were assessed: oxygen tolerance (aerobic or anaerobic) and ability to form spores. Plots of these results can be found in the folder `PhenoPlots`.

# Diversity analyses
To begin, we calculated diversity in a few different ways: first, we used beta diversity, which is often used in ecology to compare relative diversity of different communities that have some species in common. The advantage of this method is that it is both a relative term, but also allows comparison between very different communities and is a good measure of uniqueness. The module diversity.py calculates beta diversity using the asv table provided.
Next, we calculated species richness; the advantage of this metric is that it discounts abundance information, and instead is a measure of just how many unique species are in each community.
In order to characterize communities in more wholistic approach, we used ordination methods, which is a common approach in ecology to use with multivariate data. The goal is to compress multivariate data down to fewer axes while maintaining distinction between the groups of interest; in this case, we want to compare communities on a 2-D continuum, with axes that hopefully are representative of 'real' variation between communities. R package 'vegan' was used to accomplish this goal, and the module for computing and plotting NMDS results, along with species richness, are in 'nmds.R.'
We found that diversity changed insignificantly with altitude; the differences in diversity between altitudes were swamped by flight differences. This conclusion was reached using the NMDS approach; the two different diversity measures also showed no major differences between altitude groups. Thus, a possible avenue for future work is to try to better understand the difference between microbial communities in the air due to short-term wind patterns or other environmental variables.

# Distribution of individual species(or genera) across samples
The file analysis.py allows you to plot the distribution of individual species (or genera) across samples. Sample number will be the x axis and the number of individual bacteria from a specified species/genus will be plotted on the y axis. In order to change which species/genus you want to analyze, change the ASV number in the code. In  order to find out which ASV number corresponds to which species/genus, refer to the tax_table.csv file. Colors of bars are Red = Ground, Green = Troposphere, Blue = Stratosphere, Black = Control, Purple = Exterior of Aircraft PreFlight, Cyan = Exterior of Aircraft PostFlight. 

# Directory
- BacDiveR: BacDiveR submodule: a reference to the BacDiveR git repository.
- BacDiveR_rproj: An R project module where BacDive RESTful API was accessed and data pulled for futher analysis.
- PhenoPlots: Phenotype plots per condition, saved into this folder.
- aeroDADA2: A submodule that contains asvs, sequences, and metadata for 16S amplicon data collected from C-20A science flights in the troposphere and lower stratosphere. It has its own `README.md` that describes itself in more depth.
- README.md: This file!
- NMDS.R: Ordination plotting
- test_diversity.py: Beta diversity testing
