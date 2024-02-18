 + 1. Data formats supported by PCL 1.1.pcd format 1.2.ply format

 + 2. PointT form of point cloud 

 + 3. Feature descriptor 

 + 4. Determine whether it is an ordered point cloud 4.1. Code implementation 4.2. Result display

 + 5. Definition structure of PointNormal 5.1. Use of PointNormal 5.2. Use pcl :: concatenate Fields () to connect two fields 5.3. Copy XYZ information from the original point cloud 5.4. Result display

#  Data formats supported by PCL 

##  1.1. pcd format 

   The PCL library officially specifies the format, which is typically customized for point clouds. The advantage is that it supports the dimensional point type extension mechanism, which can better exert the point cloud processing performance of the PCL library. File formats include text and binary formats. The pcd format has a file header, which is used to describe the overall information of the point cloud. The data body part is composed of the Cartesian coordinates of the point, and the space is used as a separator in text mode. Example: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574225495
  ```  
>  An organized point cloud dataset is the name given to a point cloud, which resembles an organized image (or matrix) structure in which data is divided into rows and columns. Examples of such point clouds include data from stereo cameras or time-of-flight cameras. The advantage of an organized dataset is that by knowing the relationship between neighboring points (e.g. pixels), nearest neighbor operations are much more efficient, which speeds up the computation of certain algorithms in PCL and reduces the cost of the algorithm. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574225495
  ```  
##  1.2. ply format 

   A polygon file format designed and developed by Turk and others at Stanford University, and therefore also known as the Stanford Triangle format. File formats are available in both text and binary formats. A typical PLY object definition is simply a list of (x, y, z) triples of vertices and a list of faces described by the index in the vertex list. 

>  The file structure is as follows: · Header · Vertex List · Face List · (lists of other elements) 

 Example: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574225495
  ```  
#  Second, the PointT form of point cloud 

#  III. Feature descriptors 

#  IV. Determine whether it is an orderly point cloud 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574225495
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574225495
  ```  
##  4.1. Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574225495
  ```  
##  4.2. Presentation of results 

 ![avatar]( 20210530091335734.png) 

#  Definition of PointNormal 

    PointNormal is a point structure that stores XYZ data, and contains the normal and curvature of the sampling points. For more details on the point cloud format, click here. The structure of PointNormal is as follows: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574225495
  ```  
##  5.1. Use of PointNormal 

 ![avatar]( 2021050818541272.png) 

   When using pcl :: Normal Estimation to calculate the normal vector of a point cloud, if the output point cloud is in the format pcl :: Point Normal, the XYZ fields are both 0. As shown in the figure below, it is a PCD format point cloud saved as a pcl :: Point Normal structure. PCL :: Point Normal is required for point-to-surface ICP registration, curvature-based 3D-SIFT keypoint detection, index space sampling, triangulation, and other applications. There are two ways to generate pcl :: Point Normal: 

##  5.2. Using pcl :: concatenate Fields () to join two fields 

 For more on PCL :: concatenate Fields (), see: PCL point cloud merging (joining data or fields in two point clouds) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574225495
  ```  
##  5.3. Copy XYZ information from the original point cloud 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574225495
  ```  
##  5.4. Presentation of results 

 The correct PCD file for PCL :: Point Normal structure is shown below  

