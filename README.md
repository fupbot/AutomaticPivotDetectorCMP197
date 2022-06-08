# AutomaticPivotDetector_CMP197
#### A computer vision program developed to find and analyze irrigation pivot with multiespectral satellite imagery. <br />
#### Final project for the master's course of Computer Vision (CMP197) for the semester of 2021/2 at UFRGS, Brazil. <br />
#### Author: Fabio Ugalde Pereira <br />

This project had as its main goal the automatic identification of circular or partially circular patterns created by central irrigation patterns. This project can be used to quickly estimate statistics for agricultural land use, water use and geomorphological analysis. Also, given a sufficiently small periodic sattelite revisit time, this can also aid farmers in monitoring their crops for data such as status of growth, ratio of good plants, temporal crop evolution, etc. <br />

The project was developed in Python 3 using the GDAL package for image processing activities, OpenCV for image manipulation and Scikit-Learn, Numpy and Pandas for data and machine learning. <br />


**DATA:** The sattelite images of the region of interest (ROI) is gathered from the open database of **Sentinel 2** Mission of the European Space Agency. <br /> 

**WORKFLOW:** <br />
The code is structured in the following manner: <br />
1 - The user must define a shapefile of the ROI in a third-party software such as Google Earth or QGIS. This shapefile (.shx or .shp) is used to crop the Sentinel image down to only the desired region. <br />
2 - The code generates a vegetation index called 'NDVI' (Normalized Difference Vegetation Index). This calculates the normalized difference between the near-infrared and red channels of the image, and it highlights pixels that contain photosynthetically active vegetation. This highlights areas that are cultivated and it presents a limitation of this application, which can only detect pivots after a certain level of vegetation development. <br />

![comp_ndvi_bin](https://user-images.githubusercontent.com/85031646/172697303-fa25a385-e837-4052-823a-fa4c6a24a7d1.png =250x250)

3 - The NDVI image is binarized with OTSU's method. This step, applied on the NDVI image, makes soil pixels black (0) and vegetation pixels white (1). <br />
4 - In order to extract circular features, the Circular Hough Transform method of OpenCV is applied. This function has many parameters and poses an issue: if these parameters are too tight, the function misses some pivots (high false-negative rate); if these parameters are too loose, too many false-positives are found. <br />
5 - Given the constraint above, the algorithm uses a joint solution: Loose parameters with high incidence of false-positives, which are then later classified by a Random Forests machine learning algorithm. The Random Forests algorithm learns what real pivots look like and filters out false-positives. <br />
6 - The true positives found are then used to create a mask on the original RGB image and highlight the pivots found. The same mask is used to calculate area of each pivot. <br />
7 - The global and individual statistics are overlaid on the RGB image and the results are shown as the images below. <br />

![final](https://user-images.githubusercontent.com/85031646/172697468-1e4e11ec-02d8-4511-b8da-ae67f804cdd8.png =250x250)

