# IMC_Denoise & Cell Segmentation 
<ul>
  <li>Deep Learning Model Training</li>
  <li>Performance Evaluation</li>
  <li>Impacts in Downstream Analysis:
    <ul>
      <li>Cell Segmentation</li>
      <li>Marker Expression</li>
    </ul>
  </li>
</ul>

<h2>Description</h2>
This study applied an adapted version of <a href="https://github.com/PENGLU-WashU/IMC_Denoise">IMC_Denoise</a>, a self-supervised deep learning pipeline, to a multi-channel Imaging Mass Cytometry dataset of PDAC and IPMN samples with immune, stromal, and nuclear markers. The models generated denoised outputs and was evaluated using PSNR, SSIM, segmentation quality, and marker expression consistency.

<h2>Languages and Utilities for Project</h2>

- <b>Python</b> 
- <b>R</b>
- <b>Bash / C<b/>

<h2>Environment Properties for IMC_Denoise </h2>

- Windows 10 64bit
- Python 3.6
- Tensorflow 2.2.0
- Keras 2.3.1
- NVIDIA GPU + CUDA

Visit creators page for more information on installation and troubleshooting <a href="https://github.com/PENGLU-WashU/IMC_Denoise">IMC_Denoise</a>

<h2>Methods:</h2>

<h3>Clinical Samples, Data Acquisition and Pre-processing</h3>

A set of pancreatic histology clinical samples was processed by the University of Verona, by selecting 
multiple regions of interest (ROIs) and assembling them into multiple tissue microarray (TMA) slides, 
subsequently digitalised via Imaging Mass Cytometry (IMC) into an extensive data set. </h5>

This dataset was then made available to the Maiques Lab from Barts Cancer Institute (BCI), from which 371 distinct multi-channelled images of PDAC (n = 187) and IPMN (n = 184) samples, covering multiple pancreatic regions of each patient, were used for analysis. 

These TMAs were stained with labelled metal-isotope-conjugated antibodies containing, for each 
multiplexed tissue image, a total of 37 channels specific to distinct cell markers, from which 15 of them, 
targeting immune and stromal markers, were selected for this experiment.

<p align="left">
<h4> Isotope-tagged Marker Panel: </h4>
<img src="https://i.postimg.cc/mD2CJ5LT/Screenshot-2026-05-12-213425.png" height="80%" width="80%" alt="Mass Cytometry Panel"/>

<h4> Sample Folder Organisation: </h4>
<img src="https://i.postimg.cc/3JP6hgDr/Screenshot-2026-05-12-214924.png" height="80%" width="80%" alt="Sample Folder Organisation"/>

<h3>Training of Deep Learning Models</h3>

After creating a Conda environment specific to this step, the IMC_Denoise deep learning pipeline was validated using a dataset provided by the developers and subsequently tested on a small subset of the data used for this research. 

Patches were generated and visualised for each image using a function integrated in the denoising pipeline that recursively scanned through all the sample folders and selected .tiff images associated with the respective channel.

<h4> Example of Generated Patches: </h4>
<img src="https://i.postimg.cc/MGr3sVwP/Screenshot-2026-05-12-215457.png" height="80%" width="80%" alt="Generated Patches"/>

Each set of patches was subsequently used to train a DeepSNiF model for their respective channel, 
using the same parameters for all 15 models. Training epoches were increased from 50 to the default 200 for 
statistical purposes, ensuring a plateau was achieved for very noisy channels, with train batch size set to the default of 128. 

Most default parameters were ideal for this dataset, including the data split into both validation 
(15%) and training set (85%), a step readily integrated in the model training with the parameter 
“val_set_percent”.

<h4> Model Training Parameters: </h4>
<img src="https://i.postimg.cc/jSqrmHpm/Screenshot-2025-07-19-224324.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Finally, after training was completed, training and validation losses were plotted for each model in a 
Binary Cross-Entropy (BCE) losses graph, demonstrating discrepancies between training and validation, as well as giving an initial indicator of over- and underfitting.

These steps were repeated for each of the 15 marker channels.

<h4> Graph 1: </h4>
<img src="https://i.postimg.cc/bNBTf8Wb/Screenshot-2026-05-12-221344.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<h5> Graph 1) Training and validation performance of top 5 performing models based on BCE and training and validation loss curves. (A) Bar plot showing training and validation losses of the top 5 models based on BCE loss, ranked from left (top performer - DNA3) to right (lower top performer - CD45RA). (B) BCE loss line graphs demonstrating the learning curve of 4 different models (CD8, DNA3, Granzyme, CD163). </h5>

<h3> Denoising Predictions:</h3>

After training, the whole dataset was computationally predicted by the 15 DeepSNiF trained models, 
each used for their respective channel’s image set.  

To evaluate the efficiency of this model, a function was created to iteratively scan through raw image 
folders of the selected channel, pick all the .tiff files associated with it, and predict denoised images. 

While predictions were running, this function would side them by the raw image for visual comparison 
purposes and produce Peak signal-to-noise ratio (PSNR) and Structural similarity index measurement (SSIM) 
metrics, stored separately in .csv format. Metrics graphs were plotted from previously saved .csv files, and the efficiency in removing noise while preserving the tissue architecture was evaluated individually. 

Finally, following predictions, a function was built to reorganise denoised images into new folders 
specific to each sample, containing all fifteen image channels.
