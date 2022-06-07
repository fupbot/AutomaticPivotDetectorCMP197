# AutomaticPivotDetector_CMP197
A computer vision program developed to find and analyze irrigation pivot with multiespectral satellite imagery.
Final project for the master's course of Computer Vision (CMP197) for the semester of 2021/2 at UFRGS, Brazil.
Author: Fabio Ugalde Pereira

This project had as its main goal the automatic identification of circular or partially circular patterns created by central irrigation patterns. This project can be used to quickly estimate statistics for agricultural land use, water use and geomorphological analysis. Also, given a sufficiently small periodic sattelite revisit time, this can also aid farmers in monitoring their crops for data such as status of growth, ratio of good plants, temporal crop evolution, etc.

The project was developed in Python 3 using the GDAL package for image processing activities, OpenCV for image manipulation and Scikit-Learn, Numpy and Pandas for data and machine learning.


DATA: The sattelite images of the region of interest (ROI) is gathered from the open database of Sentinel 2 Mission of the European Space Agency.

WORKFLOW:
The code is structured in the following manner:
1 - The user must define a shapefile of the ROI in a third-party software such as Google Earth or QGIS. This shapefile (.shx or .shp) is used to crop the Sentinel image down to only the desired region.
2 - The code generates a vegetation index called 'NDVI' (Normalized Difference Vegetation Index). This calculates the normalized difference between the near-infrared and red channels of the image, and it highlights pixels that contain photosynthetically active vegetation. This highlights areas that are cultivated and it presents a limitation of this application, which can only detect pivots after a certain level of vegetation development.
3 - The NDVI image is binarized with OTSU's method. This step, applied on the NDVI image, makes soil pixels black (0) and vegetation pixels white (1).
4 - In order to extract circular features, the Circular Hough Transform method of OpenCV is applied. This function has many parameters and poses an issue: if these parameters are too tight, the function misses some pivots (high false-negative rate); if these parameters are too loose, too many false-positives are found. 

