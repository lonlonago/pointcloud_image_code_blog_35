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

