REX Region of interest EXtraction toolbox
Extracts values from the selected NIFTI data files at the specified Regions of Interest (ROIs)

  Developed by 
     Alfonso Nieto-Castanon
     
  This software has now been integrated with and is being further developed as part of CONN  
     
________________________________________________________________________
                                                            Installation
This software requires SPM (SPM -  http://www.fil.ion.ucl.ac.uk/spm/)
After downloading this software simply prepend the rex directory to 
your MATLAB path to complete the installation. 


________________________________________________________________________
                                                                   Usage
  rex; 
  Launches interactive GUI
 
  MEANS=rex(SOURCES, ROIS);
  where SOURCES is a list of M source volume files (image files to extract from)
  and ROIS is list of N roi files (image or .tal files)
  returns the mean values of each of the source volume files at the voxels
  identified by each ROI in the matrix MEANS (with size M x N).
 
  rex(SOURCES, ROIS, 'paramname1',paramvalue1,'paramname2',paramvalue2,...);
    permits the specification of additional parameters:
        'summary_measure' :     choice of summary measure (across voxels) [{'mean'},'eigenvariate','weighted mean','weighted eigenvariate','median','sum','weighted sum','count','max',min']
        'level' :               summarize across [{'rois'},'clusters','peaks','voxels']
        'scaling' :             type of scaling (for timeseries extraction) [{'none'},'global','roi']
        'conjunction_mask':     filename of conjunction mask volume(s)
        'conjunction_threshold' absolute-threshold defining voxels within conjunction_mask [0] (e.g. conjunction_threshold=0 or conjunction_threshold={'raw', 0} keeps all voxels with mask values above zero within each ROI; conjunction_threshold={'voxels', 10} keeps only the 10 voxels with the highest values in the conjunction mask within each ROI; conjunction_threshold={'percent', .10} keeps only voxels with top 10% values in the conjunction mask within each ROI  
        'output_type' :         choice of saving output ['none','save','savefiles',{'saverex'}]
        'gui' :                 starts the gui [{0},1] 
        'disregard_zeros'       when datatype has no NaN representation treat 0 as NaN [0,{1}]
        'roi_threshold'         absolute-threshold defining voxels within cluster [0]
        'select_clusters'       asks user to select one or more clusters if multiple clusters exists within each ROI [{0},1]
        'selected_clusters'     (for 'select_clusters'=0) indexes of clusters to select (by default this value is empty and all of the clusters will be selected) 
        'dims' :                (for 'eigenvariate' summary measure only): number of eigenvariates to extract from the data
        'covariates' :          (for 'eigenvariate' summary measure only): covariates to be regressed-out before computing svd
        'pca' :                 (for 'eigenvariate' summary measure only): PCA decomposition 1 = first extract component represents mean signal, next components represent principal component decomposition of covariance matrix); 0 = components represent SVD decomposition of the second moment (X'*X) matrix [0,{1}] 
        'mindist' :             (for 'peak' level only): minimum distance (mm) between peaks 
        'maxpeak' :             (for 'peak' level only): maximum number of peaks per cluster
        'fsanatomical' :        (for ROIs defined on freesurfer cortical surfaces): subject-specific freesurfer-generated mri/T1.nii structural file 
        'output_files':         (for output_type 'save' or 'savefiles' only): cell array of files to create {'data.txt','data.mat','roi.tal','roi.img','roi#.img'}
 
  other command-line usages:
  rex open   : opens existing rex.mat file
