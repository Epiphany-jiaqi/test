# test
测试
htmlpreview.github.io/?

Nomenclature
 
•	Through-variable:  F = force, T= torque, i=current, Q=fluid volumetric flow rate,q= heat flow rate. 
•	Across-variable:  υ = translational velocity, ω = angular velocity, υ = voltage,P = pressure, T = temperature.  
•	Inductive storage:  L = inductance, 1/k = reciprocal translational or rotational stiffness,I = fluid inertance.
•	Capacitive storage:  C= capacitance, M= mass, J= moment of inertia, Cf= fluidcapacitance, Ct= thermal capacitance. 
•	Energy dissipators:  R= resistance, b= viscous friction, Rf= fluid resistance,Rt= thermal resistance. 
The symbol v is used for both voltage in electrical circuits and velocity in translational mechanical systems and is distinguished within the context of each differential equation. For mechanical systems, one uses Newton’s laws; for electrical systems, Kirchhoff’s voltage laws. For example, the simple spring-mass-damper mechanical system shown in Figure 2.2(a) is described by Newton’s second law of motion. The free-body diagram of the mass M is shown in Figure 2.2(b). In this spring-mass-damper example, we model the wall friction as a viscous damper, that is, the friction force is linearly proportional to the velocity of the mass. In reality the friction force may behave in a more complicated fashion. For example, the wall friction may behave as a Coulomb damper. Coulomb friction, also known as dry friction, is a nonlinear function of the mass velocity and possesses a discontinuity around zero velocity. For a well-lubricated, sliding surface, the viscous friction is appropriate and will be used here and in subsequent spring-mass-damper examples. Summing the forces acting on M and utilizing Newton’s second law yields
Md2y(t)dt2+bdy(t)dt+ky(t)=r(t),(2.1)
   
Figure 2.2 (a) Spring-mass-damper system. (b) Free-body diagram.
 
Description
where k is the spring constant of the ideal spring and b is the friction constant. Equation (2.1) is a second-order linear constant-coefficient (time-invariant) differential equation.
   
Figure 2.3  RLC circuit.
 
 
Alternatively, one may describe the electrical RLC circuit of Figure 2.3 by utilizing Kirchhoff’s current law. Then we obtain the following integrodifferential equation:
v(t)R+Cdv(t)dt+1L∫0tv(t) dt=r(t). (2.2)
The solution of the differential equation describing the process may be obtained by classical methods such as the use of integrating factors and the method of undetermined coefficients [1]. For example, when the mass is initially displaced a distance  y(0)=y0 and released, the dynamic response of the system can be represented by an equation of the form
y(t)=K1e−α1tsin(β1t+θ1). (2.3)
A similar solution is obtained for the voltage of the RLC circuit when the circuit is subjected to a constant current  r(t)=I. Then the voltage is
v(t)=K2e−α2tcos(β2t+θ2). (2.4)
A voltage curve typical of an RLC circuit is shown in Figure 2.4.
   
Figure 2.4  Typical voltage response for an RLC circuit.
 
Description
To reveal further the close similarity between the differential equations for the mechanical and electrical systems, we shall rewrite Equation (2.1) in terms of velocity:
v(t)=dy(t)dt.
Then we have
Mdv(t)dt+bv(t)+k∫0tv(t) dt=r(t). (2.5)
One immediately notes the equivalence of Equations (2.5) and (2.2) where velocity  v(t) and voltage  v(t) are equivalent variables, usually called analogous variables, and the systems are analogous systems. Therefore the solution for velocity is similar to Equation (2.4), and the response for an underdamped system is shown in Figure 2.4. The concept of analogous systems is a very useful and powerful technique for system modeling. The voltage–velocity analogy, often called the force–current analogy, is a natural one because it relates the analogous through- and across-variables of the electrical and mechanical systems. Another analogy that relates the velocity and current variables is often used and is called the force–voltage analogy [21, 23].
Analogous systems with similar solutions exist for electrical, mechanical, thermal, and fluid systems. The existence of analogous systems and solutions provides the analyst with the ability to extend the solution of one system to all analogous systems with the same describing differential equations. Therefore what one learns about the analysis and design of electrical systems is immediately extended to an understanding of fluid, thermal, and mechanical systems.

2.3 Linear Approximations of Physical Systems
 
A great majority of physical systems are linear within some range of the variables. In general, systems ultimately become nonlinear as the variables are increased without limit. For example, the spring-mass-damper system of Figure 2.2 is linear and described by Equation (2.1) as long as the mass is subjected to small deflections  y(t). However, if  y(t) were continually increased, eventually the spring would be overextended and break. Therefore the question of linearity and the range of applicability must be considered for each system.
A system is defined as linear in terms of the system excitation and response. In the case of the electrical network, the excitation is the input current  r(t) and the response is the voltage  v(t). In general, a necessary condition for a linear system can be determined in terms of an excitation  x(t) and a response  y(t). When the system at rest is subjected to an excitation  x1(t), it provides a response  y1(t). Furthermore, when the system is subjected to an excitation  x2(t), it provides a corresponding response  y2(t). For a linear system, it is necessary that the excitation  x1(t)+x2(t) result in a response  y1(t)+y2(t). This is the principle of superposition.
Furthermore, the magnitude scale factor must be preserved in a linear system. Again, consider a system with an input  x(t) that results in an output  y(t). Then the response of a linear system to a constant multiple  β of an input x must be equal to the response to the input multiplied by the same constant so that the output is equal to  βy(t). This is the property of homogeneity.
A linear system satisfies the properties of superposition and homogeneity.
A system characterized by the relation  y(t)=x2(t) is not linear, because the superposition property is not satisfied. A system represented by the relation  y(t)=mx(t)+b is not linear, because it does not satisfy the homogeneity property. However, this second system may be considered linear about an operating point  x0,y0 for small changes  Δx and  Δy. When  x(t)=x0+Δx(t) and  y(t)=y0+Δy(t), we have
y(t)=mx(t)+b
or
y0+Δy(t)=mx0+mΔx(t)+b.
Therefore,  Δy(t)=mΔx(t), which satisfies the necessary conditions.
The linearity of many mechanical and electrical elements can be assumed over a reasonably large range of the variables [7]. This is not usually the case for thermal and fluid elements, which are more frequently nonlinear in character. Fortunately, however, one can often linearize nonlinear elements assuming small-signal conditions. This is the normal approach used to obtain a linear equivalent circuit for electronic circuits and transistors. Consider a general element with an excitation (through-) variable  x(t) and a response (across-) variable  y(t). Several examples of dynamic system variables are given in Table 2.1. The relationship of the two variables is written as
y(t)=g(x(t)), (2.6)
where  g(x(t)) indicates  y(t) is a function of  x(t). The normal operating point is designated by  x0. Because the curve (function) is continuous over the range of interest, a Taylor series expansion about the operating point may be utilized [7]. Then we have
y(t)=g(x(t))=g(x0)+dgdx|x(t)=x0(x(t)−x0)1!+d2gdx2|x(t)=x0(x(t)−x0)22!+⋯. (2.7)
The slope at the operating point,
m=dgdx|x(t)=x0,
is a good approximation to the curve over a small range of  x(t)−x0, the deviation from the operating point. Then, as a reasonable approximation, Equation (2.7) becomes
y(t)=g(x0)+dgdx|x(t)=x0(x(t)−x0)=y0+m(x(t)−x0). (2.8)
Finally, Equation (2.8) can be rewritten as the linear equation
y(t)−y0=m(x(t)−x0)
or
Δy(t)=mΔx(t). (2.9)
Consider the case of a mass, M, sitting on a nonlinear spring, as shown in Figure 2.5(a). The normal operating point is the equilibrium position that occurs when the spring force balances the gravitational force Mg, where g is the gravitational constant. Thus, we obtain  f0=Mg, as shown. For the nonlinear spring with  f(t)= y2(t), the equilibrium position is  y0=(Mg)1/2. The linear model for small deviation is
Δf(t)=mΔy(t),
where
m=dfdy|y(t)=y0,
as shown in Figure 2.5(b). Thus,  m=2y0. A linear approximation is as accurate as the assumption of small signals is applicable to the specific problem.
   
Figure 2.5  (a) A mass sitting on a nonlinear spring. (b) The spring force versus  y(t).
 
Description
If the dependent variable  y(t) depends upon several excitation variables,  x1(t),x2(t),…,xn(t), then the functional relationship is written as
y(t)=g(x1(t),x2(t),…,xn(t)). (2.10)
The Taylor series expansion about the operating point  x10,x20,…,xn0 is useful for a linear approximation to the nonlinear function. When the higher-order terms are neglected, the linear approximation is written as
y(t)=g(x10,x20,…,xn0+∂g∂x1|x(t)=x0(x1(t)−x10)+∂g∂x2|x(t)=x0(x2(t)−x20)+⋯+∂g∂xn|x(t)=x0(xn(t)−xn0),(2.11)
where  x0 is the operating point. Example 2.1 will clearly illustrate the utility of this method.

EXAMPLE 
2.1 Pendulum oscillator model
 
Consider the pendulum oscillator shown in Figure 2.6(a). The torque on the mass is
T(t)=MgLsinθ(t), (2.12)
where g is the gravity constant. The equilibrium condition for the mass is  θ0=0°. The nonlinear relation between  T(t) and  θ(t) is shown graphically in Figure 2.6(b). The first derivative evaluated at equilibrium provides the linear approximation, which is
 T(t)− T 0  ≅MgL     ∂sinθ  ∂θ  |  θ(t)= θ 0    (θ(t)− θ 0  ),
where  T0=0. Then, we have
T(t)=MgLθ(t). (2.13)
This approximation is reasonably accurate for  −π/4≤θ≤π/4. For example, the response of the linear model for the swing through  ±30° is within 5% of the actual nonlinear pendulum response.
   
FIGURE 
2.6 Pendulum oscillator.
 
 

2.4 The Laplace Transform
 
The ability to obtain linear time-invariant approximations of physical systems allows the analyst to consider the use of the Laplace transformation. The Laplace transform method substitutes relatively easily solved algebraic equations for the more difficult differential equations [1, 3]. The time-response solution is obtained by the following operations:
1.	Obtain the linearized differential equations.
2.	Obtain the Laplace transformation of the differential equations.
3.	Solve the resulting algebraic equation for the transform of the variable of interest.
The Laplace transform exists for linear differential equations for which the transformation integral converges. Therefore, for  f(t) to be transformable, it is sufficient that
∫0−∞|f(t)|e−σ1tdt<∞,
for some real, positive  σ1 [1]. The  0− indicates that the integral should include any discontinuity, such as a delta function at  t=0. If the magnitude of  f(t) is  | f(t) |<Meαt for all positive t, the integral will converge for  σ1>α. The region of convergence is therefore given by  ∞>σ1>α, and  σ1 is known as the abscissa of absolute convergence. Signals that are physically realizable always have a Laplace transform. The Laplace transformation for a function of time,  f(t), is
F(s)=∫0−∞f(t)e−stdt=ℒ{f(t)}. (2.14)
The inverse Laplace transform is written as
f(t)=12πj∫σ−j∞σ+j∞F(s)e+stds. (2.15)
 The transformation integrals have been employed to derive tables of Laplace transforms that are used for the great majority of problems. A table of important Laplace transform pairs is given in Table 2.3. A more complete list of Laplace tra
