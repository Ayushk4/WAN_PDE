# WAN_PDE

- Implemented [Weak Adversarial Nets](https://arxiv.org/abs/1907.08272) for solving high-dimenstional PDE.
- Formulated time dependent solution as an ODE problem, instead of numerical integration. Backpropagation by adjoint method of neural ODEs.

## Results:

1. Both Time dependent and independent PDEs converged well.
2. Re-formulating as ODE problem serves a better approximation than numerical approximation methods.
The typical method of backpropagation through ODEs is adjoint method as mentioned in [Neural Ordinary Differential Equations paper (NIPS 2018) by Chen et al.](https://arxiv.org/abs/1806.07366)
3. The intuition We can select from a wide variety of ODE solvers.
4. Faster and better convergence, but at the cost of greater memory consumption during backpropagation by Tracker.jl 

#### Elliptic Dirichlet (20 dimensions) 
Note that graph is shown about x1 and x2 axis only while keeping remaining x_i = 1 for i=3, 4, ...20

Approximated Function:

![Approx Function](https://github.com/Ayushk4/WAN_PDE/blob/master/Elliptic_dirichlet_files/dims%3D20/After_20000_Iters.png)

True Function:

![True Function](https://github.com/Ayushk4/WAN_PDE/blob/master/Elliptic_dirichlet_files/dims%3D20/True_function.png)

#### Time Dependent PDEs

Approximated Function:

![Approximate Function](https://github.com/Ayushk4/WAN_PDE/blob/master/Time_Dependent_pdes/20k_iters.png)

True Function:

![True Functions](https://github.com/Ayushk4/WAN_PDE/blob/master/Time_Dependent_pdes/true_function.png)

Absolute Difference b/w approximated function and true function:

![Absolute Difference](https://github.com/Ayushk4/WAN_PDE/blob/master/Time_Dependent_pdes/20k_iters_Absolute_Diff.png)


### Possible directions:

**Current limitation** of this approach of solving PDE is huge memory consumption while backpropagating

**Solution to the current limitation** switch autodiff backend from [Tracker.jl](https://github.com/FluxML/Tracker.jl) to [Zygote.jl](https://github.com/FluxML/Zygote.jl). This can be done when DiffEqFlux.jl and Flux.jl switches over to Zygote.jl. 

Zygote.jl uses source code transformation for reverse mode AutoDiff. This leads to faster and much less memory consumption while backpropagating when compared to Tracker.jl's Auto-diff.
