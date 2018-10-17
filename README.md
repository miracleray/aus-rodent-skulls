# Australian rodent skull morphological diversification (Chapter 3 of Thesis) - data and code
Code author: Ariel E. Marcy

To cite the paper and/or code:
> Coming soonish

As of October 2018, this is still a work in progress.

After cloning this repo, remember to either set your working directory to the aus-rodent-skulls folder on your computer, or open an RStudio project from that folder.

## Data
Landmarking data:
* 3D surface scanned meshes for all skulls in the study will be available via MorphoSource
* [Raw_Coordinates.csv](Data/Raw/3D_coords.csv) - the shape coordinates from landmarking 3D  skulls in Viewbox 
* [curve_LM_key.csv](/Data/Processed/curve_LM_key.csv) - matrix generated by author to encode relationships between curve semi-landmarks and the fixed landmarks bounding them at each endpoint. Based on template described in Figure (coming soon). Used to automatically generate the slider matrix required by *geomorph* for handling curve semi-landmarks. 

Museum metadata provided by Curators:
* [Australian Museum specimens](/Data/Raw/AM_muridae_skulls.csv)
* [Melbourne Museum specimens](/Data/Raw/MV_muridae_skulls.csv)
* [Queensland Museum specimens](/Data/Raw/QM_muridae_skulls.csv)
* [South Australian Museum specimens](/Data/Raw/SAM_muridae_skulls.csv)
* [Western Australian Museum specimens]() - coming soon

Ecological metadata:
* [Trait data from Breed & Ford 2006](/Data/Processed/in_ex_traits.csv)
    
## Analyses
The analysis workflow is broken down into smaller scripts explained below. Each script loads data created by the script before, so this workflow requires you to run the scripts in order. The intermediate data -- stored as .rda files in the /Data/Results folder -- are too large to upload to Github. All of the scripts below are in RMarkdown format (.Rmd), which can be opened in RStudio. There, you can edit and run code chunks as normal, or you can click the Knit button to create HTML versions with both code and output.

* **01-extract-data-for-analyses.Rmd** Takes landmark data from Viewbox and prepares it for analysis in *geomorph*. Extracts both 3D coordinate data as well as the metadata about each specimen stored in the filename. Separates coordinate data into two datasets based on big or small patch protocols.
* **02-run-GPA-with-sliding.Rmd** Prepares the matrices needed by *geomorph* to slide patch and curve semi-landmarks. Explains landmark naming conventions needed to use this script on different datasets. Runs GPA on both patch protocols.
* **03-find-bilateral-symmetry.Rmd** Runs GPA with bilateral symmetry and merges the symmetric shape output with centroid size data from the first GPA. Calculates variation captured by asymmetry for both patch protocols.
* **04-calculate-user-error.Rmd** Takes out replicated specimens from the shape data, finds their duplicates, and calculates user error based on repeatability for both patch protocols. 
* **05-compare-patch-protocols.Rmd** Plots PCAs colored by genus to compare the variation captured by small and big patch protocols, compares ANOVAs for shape ~ genus and shape ~ centroid size, where shape is supplied by big and small patch protocols. Generates small patch shape dataset without replicates and accompanying metadata table with Csize used for the rest of the analyses.
* **06-visualize-landmark-variation.Rmd** Allows users to view outliers and see landmarking errors. Implements Dr Thomas Guillerme's new package, landvR, to visualize landmark variation across the dataset over a PC with a color-coded heatmap. 
* **07-plot-exploratory-PCAs.Rmd** Allows users to quickly plot PCAs with point colors and shapes according to taxa or trait information provided in the metadata table. 
