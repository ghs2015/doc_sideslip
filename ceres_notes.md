## 1. questions

- [ ] Problem class // what is this?? 
- [ ] how to add multiple cost functions/`functors`?
- [ ] what is `AutoDiffCostFunction`
- [ ] what is the step size of the gradient descent optimization?
- [x] what is residual here, what differences between cost function?
- [ ] what is `CostFunction`?
- `AutoDiffCostFunction`
- `NumericDiffCostFunction`
- [ ] nonlinear least square
- [ ] How to compute the overall cost from all the individual residual blocks?
- [ ] When able to use `AutoDiffCostFunction`?
- [ ] What is the meaning of Bundle Adjustment algorithm?
  - [ ] What are observations?
  - [ ] What are predictions?
  - [ ] How to predict?
- [ ] What is Gauss-Newton Optimization?
- [ ] g2o format
- [ ] SLAM, problem and model?
	- [ ] `h` as edge? `x_i` as node?
- [ ] SLAM relationship with graph opt?

 

## notes:

- every sample can set up a result block to the problem object by creating a `CostFunction` object (specifying the mechanism of computing the gradients??)
- A `LossFunction` object is used to reduce the outliers of the fitting.
- Use `ptr[i] ` is convenient when used with template.

modules:

 

- Problem

  - `CostFunction`

- `CostFunctor` (cost function)

  - state variables, x (need initial values)

  - add residual block

- `CostFunction`
- Evaluate

  - residual

  - Jacobians

- Solver

  - problem

  - summary, options

 

- residual, the loss function, type is function objector
  - take in observations from a sample, output the computed residual



# TODO

 

- [ ] Read and understand the tutorial of Ceres Solver.

- [ ] Read and understand example 10. slam pose graph 2d 

- [ ] "slam/pose_graph_2d/pose_graph_2d.cc"



## Terms

- [ ] Rodriques’ axis-angle vector

  - [ ] Rodrigues' rotation formula
- [ ] Gauss-Newton （GN）
- [ ] Levenberg-Marquardt （LM）
- [ ] radial distortion
- [ ] Eigen quaternion
- Unary edge, binary edge, hyper edge
- parameterazation // modeling??



## Reference

- [A Tutorial on Graph-Based SLAM](http://www2.informatik.uni-freiburg.de/~stachnis/pdf/grisetti10titsmag.pdf)
- [Guass-Newton Algorithm explained by whudj](http://www.whudj.cn/?p=1122#more-1122)
- [梯度下降法(gradient descent)与牛顿法(newton’s method)求解最小值](http://www.whudj.cn/?p=1042)
- http://www.whudj.cn/
- [x] [深入理解图优化与g2o：图优化篇](https://www.cnblogs.com/gaoxiang12/p/5244828.html)
- [ ] https://www.cnblogs.com/gaoxiang12/p/4395446.html


