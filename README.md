# IMC_Denoise & Cell Segmentation 
<ul>
  <li>Deep Learning Model Training</li>
  <li>Performance Evaluation</li>
  <li>Impacts in Downstream Analysis:
    <ul>
      <li>Cell Segmentation</li>
      <li>Marker Expression</li>
    </ul>
</ul>

<h2>Project Description</h2>

This study applied an adapted version of <a href="https://github.com/PENGLU-WashU/IMC_Denoise">IMC_Denoise</a>, a self-supervised deep learning pipeline, to a multi-channel Imaging Mass Cytometry dataset of PDAC and IPMN samples with immune, stromal, and nuclear markers. 

The models generated denoised outputs and were evaluated using PSNR, SSIM, segmentation quality, and marker expression consistency. 

The segmentation was performed using <a href="https://napari.org/stable/">Napari</a> and 
BodenmillerGroup's <a href="https://bodenmillergroup.github.io/IMCDataAnalysis/">IMC Data Analysis Workflow</a>.

All the Data generation, analysis and plotting was performed by me for this project, including the creation of some pipelines that were missing to make this project go forward.

Due to the nature of this project, Raw data was compared with Denoised to assess IMC quality pre- and post-denoising. 

This required:
1. Training IMC_Denoise DL-models for each channel
2. Run model predictions
3. Generate prediction metrics (PSNR, SSIM)
4. Re-organise data by re-joining different multiplex channels of the same sample
5. Segment multiplex images (Raw vs Denoised)
6. Plot Data

Steps 2, 6 required pipeline manipulation to adapt it for my data type

Steps 3, 4 and 6 required me to develop brand new pipelines

<h2> Context </h2>

A set of pancreatic histology clinical samples was processed by the University of Verona, by selecting 
multiple regions of interest (ROIs) and assembling them into multiple tissue microarray (TMA) slides, 
subsequently digitalised via Imaging Mass Cytometry (IMC) into an extensive data set. </h5>

This dataset was then made available to the Maiques Lab from Barts Cancer Institute (BCI), from which 371 distinct multi-channelled images of PDAC (n = 187) and IPMN (n = 184) samples, covering multiple pancreatic regions of each patient, were used for analysis. 

These TMAs were stained with labelled metal-isotope-conjugated antibodies containing, for each 
multiplexed tissue image, a total of 37 channels specific to distinct cell markers, from which 15 of them, 
targeting immune and stromal markers, were selected for this experiment.

For Full Project overview please refer to <a href="https://github.com/ATCGbyH/IMC_Denoise-CellSEG/blob/main/Presentation%20FINAL%20CAN7036.pdf">Project Presentation</a>

<h2>Languages and Utilities for Project</h2>

- <b>Python</b> 
- <b>R</b>
- <b>Bash / C<b/>
- <b>Docker<b/>

<h2>Environment Properties for IMC_Denoise </h2>

- Windows 10 64bit
- Python 3.6
- Tensorflow 2.2.0
- Keras 2.3.1
- NVIDIA GPU + CUDA

Visit creators page for more information on installation and troubleshooting <a href="https://github.com/PENGLU-WashU/IMC_Denoise">IMC_Denoise</a>

<h2>Workflow:</h2>

<img src="https://i.postimg.cc/TPgvp8hn/gggg.png" height="80%" width="80%" alt="Workflow Chart"/>

<h2> Pipelines Available: </h2>

Due to HPC issues and unability to re-access, a majority of the pipelines built by me during this project were lost before getting uploaded.

<ul>
  <li>Multiplex IMC Channel Sorting <a href="https://github.com/ATCGbyH/IMC_Denoise-CellSEG/blob/main/Sorting_IMG_Function.ipynb"> pipeline </a></li>
  <li>IMC_Denoise Model Training by Channel (Example) <a href="https://github.com/ATCGbyH/IMC_Denoise-CellSEG/blob/main/IMC_Denoise_Train-Example(CD163).ipynb"> pipeline</li>
</ul>
