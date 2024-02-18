#   code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574164888
  ```  
#  III. Display of results 

 ![avatar]( 20201216214522122.jpg) 



--------------------------------------------------------------------------------

#   code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574171327
  ```  
#  III. Display of results 

 ![avatar]( 20201216213824967.png) 



--------------------------------------------------------------------------------

#  First, the code implementation 

##  Version 1 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574272496
  ```  
##  Version 2 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574272496
  ```  
##  III. Display of results 

 ![avatar]( 20200812171801914.png) 

>  The consistency of the point cloud data used here is poor, and there are still a lot of holes. In engineering applications, the registration accuracy of 10cm is required. 



--------------------------------------------------------------------------------

##  I. Precautions 

>  Only when the optimal transformation between the source point cloud and the target point cloud is known can the calculated transformation be compared with the known transformation. 

##  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574243334
  ```  
##  III. Display of results 

 ![avatar]( 20201005211250971.png) 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

>  Note: This algorithm is created by myself according to the theory of quantum mechanics, and ordinary people cannot control it!!! Use with caution!!! Consequences are at your own risk!!! 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574215186
  ```  
#  III. Display of results 

 ![avatar]( 2020090720321043.png) 



--------------------------------------------------------------------------------

#  I. Overview of algorithms 

   SampleConsensusModelPerpendicularPlane use additional angular constraints to define a model for 3D plane segmentation. The plane must be perpendicular to the user-specified axis (setAxis) until the user-specified angle threshold (setEpsAngle). In other words, the plane normal must be (close to) parallel to the specified axis. Model coefficients are defined as: 

 Code example for a plane model perpendicular to the Z axis: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574261656
  ```  
 Note: An angle > 0 must be specified in order to activate the axis angle constraint! Other operations are the same as the RANSACN fitting plane principle, specific implementation reference: PCL uses RANSAC fitting plane 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574261656
  ```  
#  III. Display of results 

 Planar vertical Z-axis:  



--------------------------------------------------------------------------------

#  Attitude estimation 

##  1. Overview of the principle 

   Formally, the goal of pose estimation is to estimate a transformation that minimizes the sum of the squared distances between each point on the object model, and the corresponding point in the scene model: In the above equation, a homogeneous representation of the points is used to allow matrix vector multiplication. Attitude estimation is often solved with a robust and outlier-tolerant approach, such as RANSAC. A common way to deal with this is based on feature correspondence, where iterations run the following: (1) Find the middle random sample point and its corresponding point in by matching the nearest neighbor of the invariant feature descriptor. (2) Use the corresponding samples to estimate the hypothesis transformation. (3) Apply the hypothesis transformation to the source point cloud. (4) Find the inner point by searching the spatial nearest neighbor between the transformed source point cloud and the target point cloud through the Euclidean distance threshold. If the number of inner points is too small, go back to step (1). (5) Re-estimate the hypothetical transformation using the inner point correspondence relationship. (6) Compute the distance between the inner point corresponding point pairs, as the final transformation if the distance reaches the minimum value so far. In many cases, the algorithm can be optimized by stopping if it falls below the predefined convergence threshold. Otherwise, the algorithm will run the specified number of iterations. After the first step of each iteration, the above RANSAC pose estimation process is modified by applying a low-level geometric constraint (for the corresponding points on the target object and the scene, according to the geometric consistency that the Euclidean distance between them in their respective spaces is constant). Specifically, the ratio between the side lengths of the virtual polygon formed by the object and the sample points on the scene model is checked. The points corresponding to the sampling of the feature are represented as the side lengths of the object polygon as follows:, the side lengths of the scene polygon are calculated in the same way. Then, the relative dissimilarity vector is calculated by the ratio between the side lengths of the polygon: if the two polygons match exactly, then = 0. Expect the maximum deviation to be below a certain threshold: Therefore, the modification to RANSAC is to insert the following steps in steps (1) and (2): Calculate the vector of dissimilarity between the side lengths of the sampled polygons, and if, return to step (1). This verification step is much less costly than implementing full geometric constraints using steps (2)~ (6), and the closer to 1, the fewer iterations; however, when noise is present, the risk of excluding the correct position is increased. Assuming that this step does not filter out the hypothetical postures of the correctly aligned model, the same probability of success can be expected, but in a much shorter time. It is clear that this assumption holds only for fairly precise geometric observations, so that the polygons are indeed equidistant. If the sensor used shows a large depth error or produces a large distortion effect, the threshold, taking into account these inaccuracies, needs to be set higher. Given the current quality of the sensor, we expect the scope of this problem to be limited. Use, thereby allowing for a 25% maximum edge length difference. Our modification of RANSAC is based on a simple criterion that false assumptions should be filtered out immediately, thus saving time to generate a greater number of hypothetical postures. The method can be considered hierarchical during the rejection of outer points phase, as the method introduces a preliminary low level of polygon-based rejection that does not require postures before the usual medial-based rejection phase. 

   Given the expected probability of success and the expected internal connection score, the formula for calculating the number of required RANSAC iterations is: in general, in step (1) sampling = 3 points, internal connection score estimate = 0.05, expected success rate = 0.99, given Technologies 37000, Euclidean internal connection threshold is set to 0.01 m, the required number of internal connection points is set to 50% of the total number of object model points. 

##  2. Algorithm overview 

   The random sampling consistency algorithm is used for point cloud registration, pcl :: SampleConsensusPrerejective This class inserts a simple but effective "pre-exclusion" step through the local invariant geometry constraint in the standard RANSAC pose estimation loop to avoid validating potentially incorrect pose assumptions. To robustly align the partial/occlusion model, the routine performs the fitting error evaluation using only inliers, i.e. points closer than the Euclidean threshold, set using setInlierFraction (). Use setSimilarityThreshold () in [0,1] to specify the number of pre-rejections or "greed" of the algorithm, where 0 means disabled and 1 means maximum rejection. setSimilarityThreshold () is the improved part of the above principle description, or the standard RANSAC registration algorithm without this line of code. 

##  3. References 

>  See the paper for the specific implementation process:

A. G. Buch, D. Kraft, J.-K. Kämäräinen, H. G. Petersen and N. Krüger. Pose Estimation using Local Structure-Specific Shape and Appearance Context. International Conference on Robotics and Automation (ICRA), 2013.使用局部结构特定的形状和外观上下文的姿态估计doc：Robust pose estimation of rigid objects 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574128568
  ```  
#  III. Parameter analysis 

#  IV. Display of results 

 ![avatar]( 20210310194627334.png) 

 The left side is before registration, and the right side is after registration. The initial position of the model point cloud and the scene point cloud  



--------------------------------------------------------------------------------

#  I. Overview of algorithms 

   The registration method that fuses the coarse registration of the 3DSC feature descriptor descriptor and the fine registration of the ICP algorithm is not much seen in the paper at present (only this one: [1] Xu Guangxuan, Pang Yajun, Bai Zhenxu, Wang Yulei, Lu Zhiwei. A Fast Point Clouds Registration Algorithm for Laser Scanners [J]. Applied Sciences, 2021, 11 (8)). However, there are quite a lot of codes on the Internet about 3DSC + ICP. After taking a look, it is basically impossible to run the correct results. This article gives the complete runnable code. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574246180
  ```  
#  III. Display of results 

 ![avatar]( da7dc335975c4b788988e76d7aaf0d48.png) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574246180
  ```  


--------------------------------------------------------------------------------

#  First, the callback function 

 registerPointPickingCallback register a callback function for the point selection event. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574170916
  ```  
>  Callback This function will be registered as the callback function of the fetch event cookie and pass the user data to the callback function 

 2. Option 2: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574170916
  ```  
>  Callback passes the member function instance instance registered as a fetch event callback to the class that implements the callback function. Cookie passes user data to the callback function 

#  Second, point selection operation 

 PCL :: visualization :: Point Picking Event 1. Get the coordinates of the click point 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574170916
  ```  
>  Gets the XYZ point coordinates of the point the user just clicked.

 X The x coordinate of the point selected by the user y The y coordinate of the point selected by the user z The z coordinate of the point selected by the user 

 2. Get the ID of the clicked point 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574170916
  ```  
>  Note: If the cloud contains NaNs points, the index returned by this function will not correspond to the original index. To get the correct index, you can clean the input cloud to remove nan, or use the Point Picking Event :: getPoint function to get the x, y, z values of the selected point, and then search the original cloud for the correct index. 

 3. Functional flow 

>  The menu bar of the main window clicks the pick three-dimensional point button to pop up the non-modal sub-window dialog box displaying the result; according to the definition of the PCL point cloud library, press and hold the Shift + left mouse button to select the data point of the visual window; set the point size to 5 and display it in red to distinguish; the console displays the three-dimensional coordinates of the point; if other points are selected, the screen rendering is refreshed, and the console coordinate display is refreshed. 

#  III. Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574170916
  ```  
#  IV. Display of results 

 ![avatar]( 2021021221251522.png) 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

   We explain how to run a B-spline fitting algorithm on a point cloud to obtain a smooth, parametric surface representation. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574196816
  ```  
#  III. Display of results 

 ![avatar]( 20200724154508861.png) 

#  IV. Error reporting and handling 

 In debug mode: 

 ![avatar]( 20200724152714216.png) 

 Code execution error: program error "Expression: vector subscript out of range" After research and investigation, this problem is due to a certain amount (variable or constant) value in the program out of bounds, different programs are different quantities, this program is filling B-spline curve fitting parameter curve_params accuracy is set to 1, can run, but the fitting accuracy is poor; 

 In Release mode, it can be executed normally. 



--------------------------------------------------------------------------------

#  First, the code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574250969
  ```  
#  III. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574250969
  ```  
#  IV. Test data 

 The test data is generated by MATLAB code, which is as follows: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574250969
  ```  
 You can verify the above C++ code by yourself, it should be noted that: 

 The rotation matrix from data1 to data2 in the test data is: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574250969
  ```  
 The translation vector is: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574250969
  ```  
 It is equivalent to the expression of C++ transformation matrix. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574250969
  ```  


--------------------------------------------------------------------------------

 + 1, call function 1 2, call function 2 

 + Handwritten implementation 

#  First, the principle of the algorithm 

   Calculate the mean and standard deviation of each field of the given point cloud data x, y, z coordinates, where the standard deviation is implemented as n-1. 

#  Second, the main function 

##  1. Call function 1 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574233129
  ```  
   Given a vector of type float, calculate the mean and standard deviation of the given point cloud data simultaneously, where the standard deviation is n-1 

##  2. Call function 2 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574233129
  ```  
   There is no essential difference between the two, both are given a vector of float type, and calculate the mean and standard deviation of the given point cloud data at the same time, where the standard deviation is n-1 

##  3. Function source code 

###  1. Function 1 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574233129
  ```  
###  2. Function 2 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574233129
  ```  
#  III. Code implementation 

###  1. Function 1 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574233129
  ```  
###  result display 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574233129
  ```  
###  2. Function 2 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574233129
  ```  
###  result display 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574233129
  ```  
   The calculation method is the same, so the result is the same!!! 

#  IV. Handwriting implementation 

   This simple calculation, although there are calling functions, may not be easy to use. So write your own code that is convenient to call. The standard deviation is n to achieve. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574233129
  ```  


--------------------------------------------------------------------------------

 + 1. Radian rotation angle 

 + 2. Angle rotation radian 

 + 3. Normalize to (-PI, PI) 

 + 4. Commonly used values 

#  First, the angle of radian rotation 

##  1. Calculation formula 

##  2. Main functions 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574224094
  ```  
>  To use this function, you need to add: #include < pcl/common/common_headers > header file or #include < pcl/common/angules.h > header file 

##  3. Sample code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574224094
  ```  
##  4. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574224094
  ```  
#  Second, the angle of rotation 

##  1. Calculation formula 

##  2. Main functions 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574224094
  ```  
>  To use this function, add: #include < pcl/common/common_headers > header file 

##  3. Sample code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574224094
  ```  
##  4. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574224094
  ```  
#  III. Normalized to (-PI, PI) 

##  1. Main function 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574224094
  ```  
##  2. Source code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574224094
  ```  
#  IV. Commonly used values 

##  1. Main function 

##  2. Sample code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574224094
  ```  
##  3. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574224094
  ```  


--------------------------------------------------------------------------------

#   code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574181101
  ```  
#  III. Display of results 

 ![avatar]( 20201216200917822.png) 



--------------------------------------------------------------------------------

#  Introduction to the algorithm 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574296553
  ```  
 PCL-like :: registration :: CorrespondenceEstimationNormalShooting calculates the corresponding point pairs between the source point cloud and the target point cloud under the minimum distance constraint by normals. The input is the source point cloud and the target point cloud, and the output is the point pair, that is, the corresponding point set between the two groups of point clouds is output. 

 key member function 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574296553
  ```  
#  III. Display of results 

 ![avatar]( 20210317202159213.png) 



--------------------------------------------------------------------------------

 Code implementation of KD tree 1. Official website example 2. K nearest neighbor search and visualization 3. Radius search and visualization 4. Hybrid search and visualization

#  Introduction to the principle 

##  1. Create a KD tree 

 ![avatar]( 20210516160551664.png) 

   A kd-tree data structure is a data structure used in computer science to organize data with several points in k-dimensional space. It is a binary search tree with other constraints. K-d trees are very useful for range searches and nearest neighbor searches. For our purposes, we usually only deal with 3-D point clouds, so all our k-d trees are 3-D. Each layer of the K-d tree uses a hyperplane perpendicular to the corresponding axis, dividing all the children along a specific dimension. At the root of the tree, all the sub-nodes will be split according to the first dimension (i.e. if the first-dimensional coordinate is less than the root, it will be in the left subtree, if it is larger than the root, then it will be obviously in the right subtree). Each layer in the tree is divided on the next dimension, returning to the first dimension once all the other dimensions have been exhausted. The most efficient way to build a k-d tree is to use a partitioning method: place the middle point at the root and everything has a smaller one-dimensional value, smaller on the left and larger on the right. Then, repeat this process on the left and right subtrees until the last tree to be partitioned consists of only one element. Figure 1 is a schematic diagram of a two-dimensional data search with k = 2. Each layer of the kd-tree is a dimension of the data, and a sub-node is used to split the dimensional data interval. The data smaller than the node value in this dimension is placed in the left subnumber, and the data larger than the node value is placed in the right subtree. Each layer of the kd-tree is separated in the next dimension of the data. When the dimensions of the data are used up, it returns to the first dimension and continues to iterate until the searched data is determined. This method reduces the time complexity to. Creating a kd-tree usually uses the median value of each dimension of the data value as the segmentation hyperplane.  

   In the process of 3D point cloud data search, kd-tree also realizes the fast retrieval of 3D point cloud data by one-dimensional hyperplane perpendicular to the point cloud and recursively dividing the space into multiple subspaces. The detailed calculation process of kd-tree in 3D point cloud is as follows: 

##  2. Neighborhood search 

 ![avatar]( 20210516163024278.gif) 

   The image below is a demonstration of how the nearest neighbor search works.  

##  3. KD-Tree class description 

   Kd-tree module mainly has class pcl :: KdTree and class pcl :: KdTreeFLANN two classes; between them is an inheritance relationship, KdTreeFLANN inherits from KdTree. 

 1. class pcl::KdTree< PointT > 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
 Destructor. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
 2. pcl::KdTreeFLANN< PointT > 

 KdTreeFLANN inherits from KdTree, so you can refer to its base class description for related function descriptions. 

##  4. Main functions 

 1.K Nearest Neighbor Search 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
   Search for k nearest neighbors for a given query point. This method does not do any bounds checking on the input index (i.e., index > = cloud.s i z e () || index < 0), and assumes that the data is valid (i.e. finite). 

 2. Radius search 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
   Searches all the nearest neighbors of a query point within a given radius. This method does not do any bounds checking on the input index (i.e., index > = cloud.s i z e () || index < 0), and assumes that the data is valid (i.e. finite). 

##  5. References 

>  [1] Andrew Moore. An introductory tutorial on kd-trees [C]//IEEE Colloquium on Quantum Computing: Theory, Applications & Implications. IET, 1991. [2] Zhang Bin. Research on automatic point cloud registration method based on keypoint matching [D]. Minnan Normal University, 2020. P47-P48 [3] doc: How to use a KdTree to search [4] PCL: pcl :: KdTree FLANN [5] Detailed explanation of KDTree 

#  Code implementation 

##  1. Example of official website 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
##  2. K-nearest neighbor search and visualization 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
##  3. Radius search and visualization 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
##  4. Hybrid search and visualization 

   In addition to K-nearest neighbor search and radius search, PCL can also perform hybrid search. It returns up to K nearest neighbors whose distance from the query point is less than a given radius. This method combines the search conditions of KNN and RNN, and is also called RKNN search in some literature. It has performance advantages in many cases. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
#  III. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574123444
  ```  
 ![avatar]( 00e16a14a98c41a8b104596bdb7834fb.png) 



--------------------------------------------------------------------------------

 + 1. Introduction to octree 1. Building octree 2. Main functions 3. References

 + 2. Code implementation 

 + 3. Visual octree 

 + 4. CloudCompare 

#  Introduction to octree 

##  1. Build an octree 

>  Octree is a tree-like data structure used to describe three-dimensional space. Each node of the octree represents the volume element of a cube, and each node has eight sub-nodes. The volume elements represented by these eight sub-nodes are added together to equal the volume of the parent node. The general center point is used as the fork center of the node. Octree is a tree-like data structure used to manage sparse 3D point clouds. Each internal node has exactly eight sub-nodes. "Intra-voxel nearest neighbor search", "K nearest neighbor search", "Intra-radius nearest neighbor search" can be implemented 

 ![avatar]( 20210522212717363.png) 

 The principle of octree construction: (1) Set the maximum recursion depth. (2) Find the maximum size of the scene and build the first cube with this size. (3) Throw the unit elements into the cube that can be contained and has no sub-node in sequence. (4) If the maximum recursion depth is not reached, subdivide it into eight equal parts, and then divide all the unit elements contained in the cube into eight sub-cubes. (5) If it is found that the number of unit elements assigned to the child cube is not zero and is the same as the parent cube, the child cube stops being subdivided, because according to the space division theory, the subdivided space must be allocated less. If the number is the same, then the number of cuts is still the same, which will cause infinite cuts. (6) Repeat 3 until the maximum recursion depth is reached. The data structure of an octree, the nodes of an octree are divided into three categories: 

   For non-leaf nodes, the data structure is partitioned by octet method and decomposed into smaller sub-blocks. Each block has a node capacity. When the node reaches the maximum capacity, the node stops splitting. 

##  2. Main functions 

 1. Voxel Search 1.1 Search for neighbors within a voxel at a given point. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574199849
  ```  
 True if leaf nodes exist; otherwise, "false". 

 1.2 Search for neighbors within a voxel at the point referenced by the point index. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574199849
  ```  
 True if leaf nodes exist; otherwise "false". 2. K Nearest Neighbor Search 2.1 Search for k nearest neighbors at the query point 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574199849
  ```  
 2.2 Search for k nearest neighbors at a given query point. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574199849
  ```  
 2.3 Search for k nearest neighbors at the query point. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574199849
  ```  
 3. Radius search 3.1 Call method 1 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574199849
  ```  
 3.2 Call method 2 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574199849
  ```  
 3.3 Call method 3 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574199849
  ```  
##  3. References 

>  [1] doc：Spatial Partitioning and Search Operations with Octrees [2] PCL：pcl::octree::OctreePointCloudSearch 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574199849
  ```  
#  Visual octree 

 ![avatar]( 20210330211911392.jpg) 

#  CloudCompare 

 ![avatar]( 20201229103224953.gif) 

 Related operations in CloudCompare software: Octree > Compute: Force the calculation of an octree for a given entity Octree > Resample: Resample by replacing all points within each octree cell  



--------------------------------------------------------------------------------

#  一、PlaneClipper3D 

##  1. Introduction 

   PCL :: Plane Clipper 3D provides an implementation of a 3D plane clipper. 

##  2. Main functions 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574163024
  ```  
 Split the point cloud space using an arbitrary plane. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574163024
  ```  
 Using a straight line composed of any two points to divide the point cloud, the official website says that this function is not implemented. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574163024
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574163024
  ```  
 A polymorphic method that clones the underlying clipper with its arguments. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574163024
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574163024
  ```  
 Get the input vector of the plane parameter plane_ params. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574163024
  ```  
 Crop out the interface of a single point: true if the point is clipped out, false if the point is not in the clipping space. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574163024
  ```  
 Crop the interface of a line segment by entering the start point from and end point to of the line segment. Returns true if the line segment is clipped, and false if the line segment is outside the clipping space. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574163024
  ```  
 Provides an interface for clipping a flat polygon through an ordered list of points. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574163024
  ```  
 Provides an interface for clipping a flat polygon through an ordered list of points. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574163024
  ```  
 Interface for clipping point clouds 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574163024
  ```  
 A polymorphic method that clones the base clipper using its parameters. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574163024
  ```  
#  III. Display of results 

 ![avatar]( 791fbf68fc498b848e0773773d1c3503.gif) 



--------------------------------------------------------------------------------

 + 1. 1. Algorithm Overview 2. Algorithm Flow

 + 2. Ordinary code 

 + 3. Results display 

 + 4. Display method 

 + 5. Advanced Code 

 + 6. Advanced Results 

#  First, the principle of the algorithm 

##  1. Algorithm overview 

    On the basis of learning the greedy projection triangulation algorithm in PCL, this blog realizes the application case of using color point cloud to rebuild color model. 

>  Introduction to the principle of triangulation: Delaunay triangulation and matlab examples Fast triangulation of unordered point clouds Using greedy projection triangulation algorithm to triangulate directed point clouds PCL :: GreedyProjectionTriangulation 

##  2. Algorithm flow 

>  The specific methods are: (1) First project the directed point cloud into a local two-dimensional coordinate plane (2) Triangulate in the coordinate plane (3) Obtain a triangular mesh surface model according to the topological connection relationship of three points in the plane. 

   The three-dimensional points are projected to a plane through the normal, and then the projected point cloud is triangulated in the plane to obtain the connection relationship of each point. In the process of triangulation of the plane area, the spatial area growth algorithm based on Delaunay is used. The method selects a sample triangle piece as the initial surface and continuously expands the boundary of the surface to form a complete triangular mesh surface. Finally, the topological connection between the original three-dimensional points is determined according to the connection relationship of the projected point cloud, and the resulting triangular grid is the reconstructed surface model. The greedy projection triangulation algorithm is a fast triangulation algorithm for the original point cloud. The algorithm assumes that the surface is smooth and the point cloud density changes uniformly, and the surface cannot be smoothed and repaired while triangulation. The advantage of this algorithm is that it can handle scattered point clouds from one or more scanners and has multiple connections. However, the algorithm also has certain limitations. It is more suitable for the case where the sampling point cloud comes from a continuous smooth surface and the point cloud density changes uniformly. 

#  Ordinary code 

 This is the code that has been widely circulated on the Internet, and this code cannot reconstruct the color model. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574263202
  ```  
#  III. Display of results 

 ![avatar]( 7c455d813b174685a5fdb5695083e6ea.png) 

#  IV. Display method 

>  Note: The PCL mesh model has three optional display modes, namely surface mode (Surface) display, wireframe mode (Wireframe) display, and point mode (Points) display. The default is face mode for display. The setting functions are in order: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574263202
  ```  
 When using, just add the following when you are visual: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574263202
  ```  
#  V. Advanced Code 

 Reconstruction of color models using color point clouds 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574263202
  ```  
#  VI. Advanced results 

 ![avatar]( 43d933d328874467b3429be19f139f29.png) 



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

