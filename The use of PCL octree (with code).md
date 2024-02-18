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

