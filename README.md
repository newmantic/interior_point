# interior_point


Interior-Point Methods are a class of algorithms used to solve linear programming (LP) and nonlinear convex optimization problems. Unlike the Simplex method, which operates on the boundary of the feasible region, Interior-Point Methods work by iteratively moving through the interior of the feasible region toward the optimal solution.


Consider a standard linear programming problem in the following form:
Minimize:    c^T * x
Subject to:  A * x <= b
             x >= 0
Where:
c is the cost vector.
x is the vector of variables.
A is the matrix of constraints.
b is the right-hand side vector.
The goal is to find the vector x that minimizes the objective function c^T * x while satisfying the constraints A * x <= b and x >= 0.

The set of all points x that satisfy the constraints A * x <= b and x >= 0 is called the feasible region. Interior-Point Methods work within this region, avoiding the boundaries initially.

Barrier Functions:
A key idea in Interior-Point Methods is to introduce a barrier function that penalizes solutions close to the boundary of the feasible region. A common choice is the logarithmic barrier:
phi(x) = -sum(log(x_i))
The barrier function ensures that the algorithm stays within the interior of the feasible region.

Central Path:
The central path is a trajectory that the algorithm follows, guided by both the objective function and the barrier function. The algorithm iteratively moves along this path towards the optimal solution.

KKT Conditions:
The optimal solution must satisfy the Karush-Kuhn-Tucker (KKT) conditions:
A * x = b
s = c - A^T * z
x_i * s_i = 0,  for all i
x_i >= 0, s_i >= 0, for all i
Here, s are the slack variables, and z are the dual variables (Lagrange multipliers).

One of the most commonly used Interior-Point Methods is the Primal-Dual Interior-Point Method.

Initialization:
Start with an initial feasible point x^(0) and positive vectors s^(0) and z^(0) for slack and dual variables, respectively.

Iterative Update:
At each iteration k, solve the following system of equations (the KKT system):
A * delta_x = b - A * x^(k)
A^T * delta_z + delta_s = c - A^T * z^(k)
s^(k) * delta_x + x^(k) * delta_s = -x^(k) * s^(k) + mu^(k)
Here, delta_x, delta_s, and delta_z are the updates to x, s, and z, respectively, and mu^(k) is a centering parameter.

Line Search:
Perform a line search to determine the step size alpha that ensures the new point (x^(k+1), s^(k+1), z^(k+1)) remains feasible.

Convergence:
Repeat the iterative update until the KKT conditions are satisfied within a specified tolerance. At this point, x^(k) is the optimal solution.


Barrier Function Approach
Instead of solving the problem directly, we approximate it using a barrier function:
Minimize:    c^T * x + mu * phi(x)
Subject to:  A * x <= b
Where:
mu is a small positive parameter that controls the trade-off between optimizing the objective and maintaining feasibility within the interior.
As mu approaches zero, the solution to the barrier problem approaches the solution to the original problem.


Time Complexity
The time complexity of Interior-Point Methods is generally polynomial in the number of variables and constraints, making them efficient for large-scale linear programming problems. The complexity is often expressed as O(n^(3/2) * L) where n is the number of variables and L is the number of bits needed to represent the input data.

