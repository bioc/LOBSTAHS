# LOBSTAHS

Repo for the R package "LOBSTAHS," developed in the Van Mooy Lab at Woods Hole Oceanographic Institution. LOBSTAHS (Lipid and Oxylipin Biomarker Screening Through Adduct Hierarchy Sequences) is a multifunction package for screening, annotation, and putative identification of mass spectral features in large, HPLC-MS lipid datasets. A general workflow for feature screening and identification using LOBSTAHS is described below.

<h4>Citation</h4> 
LOBSTAHS is described in Collins, J.R., B.R. Edwards, H.F. Fredricks, and B.A.S. Van Mooy, "Untargeted discovery and identification of oxidative stress biomarkers using a lipidomics pipeline for complex datasets"

<h4>Dataset preparation in xcms and CAMERA</h4> 
Data files must be assembled into a CAMERA xsAnnotate object prior to analysis with LOBSTAHS. Scripts are provided in the [Van Mooy Lab Lipidomics Toolbox](https://github.com/vanmooylipidomics/LipidomicsToolbox) for preparing HPLC-ESI-MS data from an Orbitrap Exactive mass spectrometer in [xcms](https://bioconductor.org/packages/release/bioc/html/CAMERA.html) and then [CAMERA](https://bioconductor.org/packages/release/bioc/html/CAMERA.html). Or, the user can use his/her own implementation of xcms and CAMERA. We have successfully used the [IPO](https://github.com/glibiseller/IPO/) package to optimize xcms and CAMERA settings for a variety of datasets.

<h4>In silico database generation</h4> 
In silico data for a wide range of lipids, oxidized lipids, and oxylipins are then generated from user-supplied structural criteria using the database generation function **generateLOBdbase**. The function pairs these in silico data with empirically-determined adduct ion abundance rankings for the major lipid classes. Users can generate their own matrices of structural property ranges to be considered during a generateLOBdbase simulation using the Microsoft Excel spreadsheet templates provided in https://github.com/vanmooylipidomics/LOBSTAHS/tree/master/data-raw. (Users should generate .csv files from this Excel spreadsheets.) Ranges of values can be specified for: 

   * oxidation state,
   * total acyl carbon chain length, and
   * degree of acyl carbon chain unsaturation (i.e., number of double bonds)

Alternatively, users may load the LOBSTAHS default databases. These contain entries for a wide range of intact polar diacylglycerols (IP-DAG), triacylglycerols (TAG), polyunsaturated aldehydes (PUAs), free fatty acids (FFA), and common photosynthetic pigments. These default databases contain data on 13,578 and 11,073 unique compounds that can be identifed in positive and negative ion mode data, respectively. 

<h4>Identification, screening, and annotation using orthogonal criteria</h4> 
The function **doLOBscreen** is then used to assign putative compound identities from these in silico databases to peakgroups in any high-mass accuracy dataset that has been processed using [xcms](https://bioconductor.org/packages/release/bioc/html/CAMERA.html) and [CAMERA](https://bioconductor.org/packages/release/bioc/html/CAMERA.html). doLOBscreen then applies a series of user-selected orthogonal screening criteria based on

   * adduct ion formation patterns,
   * chromatographic retention time, and
   * fatty acid chain length (i.e., even versus odd total number of acyl carbonb atoms),

to evaluate and assign confidence scores to this list of preliminary assignments. During the screening routine, doLOBscreen *rejects assignments that do not meet the specified criteria*, identifies *potential isomers and isobars*, and *assigns a variety of annotation codes* to assist the user in evaluating the accuracy of each assignment. Results can be extracted and/or exported to file using the **getLOBpeaklist** function.

<h4>Example dataset</h4> 
The package [**PtH2O2lipids**](https://github.com/vanmooylipidomics/PtH2O2lipids/) contains a example dataset with which users can familiarize themselves with LOBSTAHS. The dataset contains both a CAMERA "xsAnnotate" object and the LOBSTAHS "LOBSet" generated from it using **doLOBscreen**. Processing of the dataset is described in Collins, J.R., B.R. Edwards, H.F. Fredricks, and B.A.S. Van Mooy, "Untargeted discovery and identification of oxidative stress biomarkers using a lipidomics pipeline for complex datasets." The dataset itself is from the paper [Graff van Creveld, et al., 2015, "Early perturbation in mitochondria redox homeostasis in response to environmental stress predicts cell fate in diatoms," ISME Journal 9:385-395](http://www.nature.com/ismej/journal/v9/n2/full/ismej2014136a.html).

LOBSTAHS is maintained by [Jamie Collins](https://github.com/jamesrco). LOBSTAHS replaces the "old" Van Mooy Lab lipidomics pipeline, which has been moved to https://github.com/vanmooylipidomics/old_pipeline.
