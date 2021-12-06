### Output of Fastsurfer:

#### Folder Structure:
```
/home/user/FastSurfer/output
├── subject1
├── subject2
├── subject3
…
│
├── subject19
    ├── mri
    │   ├── aparc.DKTatlas+aseg.mgz
    │   ├── aseg.auto_noCCseg.mgz
    │   ├── orig.mgz
    │   ├── …
    │   …
    ├── scripts
    │	├── recon-all.log
    │	├── …
    │	…   
    ├── stats
    │	├── aseg.stats
    │	├── …
    │	…   
    ├── surf
    ├── tmp
    ├── touch
    └── trash
```

Folder explaination:
 Important ones:
    TEts
* __mri__: here are Stored the output files:
    	Important ones:
    		- aparc.DKTatlas+aseg.deep.mgz:
				output of segmentation of FasSurferCNN (input for recon_surf pipeline) 
    		- aparc+aseg.orig.mgz:
    			input segmenation for recon_surf is converted to .mgz (in default pipeline it is already a .mgz so it is just a copy of segmentation of FasSurferCNN) 
    		- aparc.DKTatlas+aseg.deep.withCC.mgz:
    			A few steps into recon-surf we use FreeSurfer to compute the Corpus Callosum label. This label then gets painted into the orignial FastSurferCNN segmentation.
    		-aparc.mapped+aseg.mgz:
    			This file is an updated segmentation (including CC), where the cortical regions (aparc) are mapped from the surfaces back into the volume. Generally a "mapped" in the file name indicates that cortical parcellations are not computed on the cortical surfaces but are mapped from the CNN segmentation onto the surface earlier, e.g. for ROI thickness estimates. The aparc.mapped+aseg.mgz is a volume where both subcortical and cortical labels are corrected by the surfaces, so that no cortical labels should be outside the space between white and pial surface. From this segmentation volume we create a wmparc.mapped.mgz including the additional white matter segmentations. Similarly the aseg.mgz (without cortical parcellations) is updated with the surfaces.
    		-aparc+aseg.mgz (OPTIONAL --fsaparc):
    			If recon-surf was run with the --fsaparc flag, processing is more involved. Here we use FreeSurfers non-linear spherical atlas to actually segment surfaces as done in FreeSurfers recon-all, instead of only mapping FastSurferCNN's volume segmentation onto the cortex. This adds considerable processing time mainly and provides the aparc+aseg.mgz and wmparc.mgz files.
    			The spherical registration step, however, is necessary if users want to perform statistics on the surfaces (fsaverage as a group template). It can be switched on by itself without spherical segmentation, via the --surfreg flag.
    
* __scripts__: here are stored the .log files of the run pipeline. Important ones:
    
    	- deep-seg.log (Log file for fastsurfercnn eval.py)
    	- recon-all (whole pipeline: FastSurferCNN + recon-surf,)
    	- recon-surf Log file for recon-surf.sh)
    	...
    	
* __stats__ : Here are computed and provided some Statistics:
    	
    	- aparc.DKTatlas+aseg.deep.volume.stats (stats for aparc.DKTatlas+aseg.deep.withCC.mgz)
    	- wmparc.mapped.stats (white matter segmentation stats)
    	- aseg.stats (Final aseg stats)
    	...
 Other:
    __surf__ ?
    __tmp__ ?
    __touch__ ?textfiles with commands which are runed at runtime ? 
    __trash__ ?
    __label__ ?

	
#### FreeSurfer:

FreeSurfer is a set of software tools for the study of cortical and subcortical anatomy. In the cortical surface stream, the tools construct models of the boundary between white matter and cortical gray matter as well as the pial surface. Once these surfaces are known, an array of anatomical measures becomes possible, including: cortical thickness, surface area, curvature, and surface normal at each point on the cortex. The surfaces can be inflated and/or flattened for improved visualization. The surfaces can also be used to constrain the solutions to inverse optical, EEG and MEG problems. In addition, a cortical surface-based atlas has been defined based on average folding patterns mapped to a sphere. Surfaces from individuals can be aligned with this atlas with a high-dimensional nonlinear registration algorithm. The registration is based on aligning the cortical folding patterns and so directly aligns the anatomy instead of image intensities. The spherical atlas naturally forms a coordinate system in which point-to-point correspondence between subjects can be achieved. This coordinate system can then be used to create group maps (similar to how MNI space is used for volumetric measurements).

FreeSurfer has several interactive graphical tools for data visualization, analysis, and management. The primary GUI is called Freeview. This tool has many functionalities, which include: visualizing FreeSurfer outputs (surfaces, volumes, ROIs, time courses, overlays and more), editing FreeSurfer-generated volumes, segmentations and parcellations, as well as the ability to manually label MRI data. FreeSurfer also has a GUI to assist in the management and analysis of groups of data, called QDEC.


