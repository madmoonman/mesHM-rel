# mesHM

A Free GUI to Control OpenFOAM Mesher SnappyHexMesh

**Author:** Michael Hiller

**Version:** 2.0 (dev)

**Software Versions**    

* Python 3.6.5
* VTK 9.0.1
* PyQt5

**Targeted OpenFOAM release**
* OF Foundation
* ESI OpenFOAM v1812 or more recent

## Philosophy
*mesHM* was build with the following intensions: unlike creating valid snappyHexMeshDicts from scratch - which is
quite simple - this tool aims to not only write valid dictionaries, but also read and reuse them. Since all the
information needed for the case is stored here, it is apparent to read it again instead of storing stuff 
externally. Consequently, mesHM reads the dictionaries and presents the most important stuff in a GUI. Here the user
is able to edit settings, refinement levels, create or delete regions. Once everything is set, an update is 
triggered and the original dictionaries are appended with the new information. A key aspect of the development
from the first day was, to **edit what is supported and leave what is not supported**. What does this mean? It means,
it is impossible to support all the functionality of snappyHexMesh right away, or, ever really. So the focus is set
on certain aspects and change only the corresponding parts. An example: the user should be able to change the 
surface refinement levels for a region of a triSurfaceMesh. In the dictionary, there will be a subdictionary called
"regions". But maybe there is another entry, where the user provided the scale for the file. For reasons
the scale shouldn't be in the GUI. So it is kept internally and written out again when updating the file.
That way, the file remains editable by the user in a text editor for everything that is not 
supported but also editable in the GUI for everything that is implemented. 
Maximum flexibility. Also this allows me to add further functionality over time without destroying
valid dictionary entries merely because the features are not supported yet.

*mesHM* is intended as a stand-alone software with no external dependencies. 

## Main features
### snappyHexMeshDict
- Change the most important global settings
- locationInMesh
    - Check locationInMesh validity
    - Generate valid locationInMesh
- triSurfaceRegions (currently only for the main region)
    - Define edge refinement level
    - Define surface refinement levels
    - Define boundary layers
- refinement regions
    - Define bounds
    - Define target levels

### blockMesh
* blockMeshEstimator
  * calculates size of blockMesh for a bounding box based (3b) approach

### surfaceFeatureExtractDict
* Read defined edge refinement
* Update the dictionary with the needed entries

### GUI
* Visualize geometry and refinement regions in the embedded, interactive vtk-render view

## Planned Major Features and Improvements
* On-demand JSON export
* Further, fully supported refinement region types (spheres, cylinders)
* Create valid blockMeshDict for 3b-approach
* Generally improved error-handling, logging, output
    
## Change-Log
### Version 2.0.11, 2022/02/08
When browsing a new directory, the dialog will open up the father dir of the latest case instead of the case itself
Check existence and try to create the mesHM_data folder if not present, was missing in this version
Fixed crash when no comment indicators were present in definition line of refinement regions
Fixed issue where in GUI deleted refinement regions with invalid input would stop update routine with nothing to do for the user
but reloading and loosing his work of the session

### Version 2.0.10, 2022/01/17
Mitigated issues with surfaceFeatureExtractDict and features subdictionary in sHMD when there were deleted patches still present
Order patches alphanumerically
Min/Max surface refinement is now also changing the patch-specific setting in the UI
LocationInMesh is now checked upon file update routine. Update is stopped, when location is outside
More robust reading of refinement regions

Minor adjustments:  
Added a ton of logging
tolerance spinbox now increments 0.1
More descriptive tool tips in refinementRegions

### Version 2.0.9, 2021/12/22
Fixed a bug, when updating sHMD and sFED separately, newly created refinement regions would be created twice
The browse dialog in the launcher now defaults to the latest used directory instead of installation dir

### Version 2.0.8, 2021/12/14
surfaceFeatures relating to a deleted patch in the main STL file will now be automatically removed from surfaceFeatureExtractDict
internal cosmetic changes to the logging output

### Version 2.0.7, 2021/12/10
New feature: copy bounding box of a patch or refinement region and paste to other refinement region

### Version: 2.0.6, 2021/12/01
Error message instead of crash, when trying to open a recent case that was deleted/moved/renamed
Internal fix: number of recent paths as specified in the settings is now used (was default value of 8)
Abort export for surfaceFeatureExtractDict, if needed stl files are not present

### Version: 2.0.5, 2021/11/25
Replaced all output tabs with 4 spaces, also 4 spaces are filtered out when reading the files  
blockMeshEstimator now shows sizes of levels 1, 2 and 3  
New loading bar during reading/setup of the case indicates the application is working
Fixed wrong processing of steps to run (castellatedMesh, snap, addLayers)

### Version: 2.0.4, 2021/11/08
Fixed wrong processing of "relativeSizes" entry in addLayers subdictionary

### Version: 2.0, 2021/11/02
Original release with new Qt GUI, VTK renderer and overhauled core implementation.

## Getting Started
1. Download whole versioned folder, preferably take out the "mesHM" folder and put it to wherever you prefer (no installation needed)
2. Run the contained mesHM.exe in Windows
	a) If it crashes right away: In your user directory, create a folder called 'mesHM_data'. On a Windows machine, it may look like C:\users\<yourname>\mesHM_data
	b) Retry running the executable