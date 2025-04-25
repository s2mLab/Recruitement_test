# Recruitment test
- Install [bioptim](https://github.com/pyomeca/bioptim) (a Linux environment is highly recommended)
- Modify the [example](https://github.com/pyomeca/bioptim/blob/master/bioptim/examples/getting_started/pendulum.py) bioptim/examples/getting_started/pendulum.py as follows:
include a double pendulum with one y-translation (range -2 to 2) and two x-rotations (range -10 pi to 10 pi). 
  - Compare files: bioptim/examples/getting_started/modelspendulum.bioMod and
  bioptim/examples/getting_started/models/double_pendulum.bioMod to create the requested model. 
    ```
    bio_model = BiorbdModel(biorbd_model_path)
    bio_model.nb_q # should give 3
    ```
  - Adapt the initial state to have the two pendulums hanging and the final state to have the two pendulums vertically up.  
    - You can determine your initial and final states visually (use the sliders or set the coordinates).
    - You may also validate that the degrees of freedom correspond to horizontal translation and rotations in the plane yOz
    ```
    import bioviz
  
    bioviz.Viz(biorbd_model_path).exec()
    ``` 
      or 
    ``` 
    import bioviz
    import numpy as np
     
    biorbd_viz = bioviz.Viz(biorbd_model_path) # load model
    biorbd_viz.set_q([0, np.pi/5, 0])  # provide the three dof values
    ```

- If you use Bound_List() to define the initial and final state, you should have:
  ```
    x_bounds["q"].min
    #PathCondition([[  0.        ,  -2.        ,   0.        ],
    #               [  0.        , -31.41592654,   3.14      ],
    #               [  0.        , -31.41592654,   0.        ]])
  
    x_bounds["q"].max
    #PathCondition([[ 0.        ,  2.        ,  0.        ],
    #               [ 0.        , 31.41592654,  3.14      ],
    #               [ 0.        , 31.41592654,  0.        ]])
  ```   
  You can also use constraints.
 
- Adapt the bounds of the control to [-150, 150] N for the degree of freedom in translation and [-2, 2] Nm for both degrees in rotation. 
If you use Bound_List() to define the bounds on the controls, you should have:
  ```` 
  u_bounds["tau"].min
  #PathCondition([[-150., -150., -150.],
  #               [  -2.,   -2.,   -2.],
  #               [  -2.,   -2.,   -2.]])
  
  u_bounds["tau"].max
  #PathCondition([[150., 150., 150.],
  #               [  2.,   2.,   2.],
  #               [  2.,   2.,   2.]])
  ````
- Modify the cost function to minimize quadratic forces (joint 0) with a weighting of 1; and quadratic torques (joints 1 and 2) with a weighting of 500 using Lagrange terms. 
- Solve the problem with 100 nodes using a direct collocation scheme (instead of a 4th order Runge-Kutta method)
- Provide a concise report that includes:
  - The mathematical expression of the optimal control problem and a comprehensive explanation of this problem
  - Based on the figures, a brief description of kinematics and efforts of the optimal strategy. Why does it make sense?
  - Send the Python script and the model file.

You may contact [M. Begon](mickael.begon@umontreal.ca) for a 10-min meeting for troubleshooting.
 
 