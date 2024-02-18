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

