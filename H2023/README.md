# Recruitment test
A pdf report should be given to your contact person when the test is completed.

- Follow the instructions to install [bioptim](https://github.com/pyomeca/bioptim) on your computer.
- Download the entire repository and run the recruitment_script.py script on your computer. What is the error message displayed in your console.
- A bug is hidden in the script; find it, modify it, to make the script work, explain in one or two sentences why it did not work (hint: the file bioptim/misc/enums.py will be useful)
- Modify the code to minimize the time of the optimal problem. Add a screenshot of the code changes in the report and the resulting time of the optimal control program. (hint: the file bioptim/examples/optimal_time_ocp/pendulum_min_time_Lagrange.py will be useful)
- Summarize in a few sentences what the simulation did and what the time minimization adds to the original problem. (Hint: use the graphs generated with sol.graph() to support your explanation).
- Plot the controls (`sol.controls["tau"]`) and the position of the pendulum (`sol.states["q"]`) to compare the results with and without time minimization. (Hint: the file bioptim/examples/getting_started/example_save_and_load.py will be useful to save both configurations).
- explain in two or three sentences what the differences are. 
