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
### Version: 2.0, 2021/11/02
Original release with new Qt GUI, VTK renderer and overhauled core implementation.

## Getting Started
1. Download zipped archive and extract to a location of your choice
2. In your user directory, create a folder called 'mesHM_data'. On a Windows machine, it may look like C:\users\<yourname>\mesHM_data
3. Launch the program using the executable