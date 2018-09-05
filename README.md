# iRODS-ETL-ImagePlot
Metadata extraction, transformation and load scripts for the iRODS pilot Imaging and Plotting use cases

## Imaging use case
In this use case, researchers use a piece of equipment to make high resolution images. In addition to an image file, the equipment produces a text file that contains metadata describing input parameters for an observation.

The image and text files were loaded into iRODS using Cyberduck. The Image_generate_metadata notebook reads the text files and generates the iCommands needed to add the metadata to the image files in iRODS.

## Plotting use case
In this use case, researchers use a different piece of equipment to take multiple measurements in a 3D parameter space. The result is a table with several measurement values at each point in 3D parameter space. This piece of equipment produces 3 files per experiment: a data file containing the table of values, a ‘set’ file containing the experiment metadata and a ‘metadata’ file with additional metadata from the table of values file.

The Plot3D_01_fill_iRODS notebook loops over files on an external USB disk searching for complete sets of data. It then generates plot files for each measurement in the table file and it also generates a text file with the iCommands needed to add the metadata to an iRODS collection. Finally it creates an iRODS collection and copies the complete set of files to it. iRODS is mapped to a disk drive using davrods.

The Plot3D_02_fill_iRODS notebook adds some additional plot data to the generated plots. Ideally this should be incorporated into the first notebook. It does not use iCommands, but connects to iRODS using the Python API.

The Plot3D_03_fill_iRODS notebook removes metadata who's values were set to the string 'None'. It also corrects some end of line problems caused by running the original notebook under Windows. Ideally this should also be incorporated into the first notebook. This notebook does not use iCommands, but also connects to iRODS using the Python API.
