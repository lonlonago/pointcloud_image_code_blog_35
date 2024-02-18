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

