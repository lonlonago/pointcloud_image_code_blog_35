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

