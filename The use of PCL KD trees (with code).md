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

