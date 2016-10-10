#Approximate a circle with cubic Bézier curves  
link:[http://spencermortensen.com/articles/bezier-circle/](http://spencermortensen.com/articles/bezier-circle/)  
>A good cubic Bézier approximation to a circular arc is:  
P0 = (0,1), P1 = (c,1), P2 = (1,c), P3 = (1,0)  
**c = 0.551915024494**  
This yields an arc on the unit circle centered about the origin, starting at P0 and and ending at P3, with the least amount of radial drift.


Bézier curves are often used to generate smooth curves because Bézier curves are computationally inexpensive and produce high-quality results. The circle is a common shape that needs to be drawn, but how can the circle be approximated with Bézier curves?  
The standard approach is to divide the circle into four equal sections, and fit each section to a cubic Bézier curve. This reduces the problem to a matter of fitting a cubic Bézier curve to a right circular arc.  
The standard approach imposes the following constraints:  
1. The endpoints of the cubic Bézier curve must coincide with the endpoints of the circular arc, and their first derivatives must agree there.  
2. The midpoint of the cubic Bézier curve must lie on the circle.  
The general formula of a cubic Bézier curve is:  
B(t) = (1-t)^3*P_0 + 3*(1-t)^2*t*P_1 + 3*(1-t)*t^2*P_2 + t^3*P_3, t in [0,1]  
The first constraint implies that:  
P_0 = (0,1), P_1 = (c,1), P_2 = (1,c), P_3 = (1,0)  
The second constraint provides the value of c:  
c = (4/3)*(sqrt(2) - 1)  
This gives the approximation:  
c = 0.5522847498  
The maximum radial drift is 0.027253% with this approximation.  
In this approximation, the Bézier curve always falls outside the circle, except momentarily when it dips in to touch the circle at the midpoint and endpoints.  
![pic1](http://spencermortensen.com/articles/bezier-circle/.page/standard.gif)  
The Bézier curve touches the right circular arc at its initial endpoint, then drifts outside the arc, inside, outside again, and finally returns to touch the arc at its endpoint.  
Figure 2. The radial distance from the arc to the standard Bézier approximation.
A better approximation  
However, a better approximation is possible if we replace the final constraint with a new constraint:  
The endpoints of the cubic Bézier curve must coincide with the endpoints of the circular arc, and their first derivatives must agree there.  
The maximum radial distance from the circle to the Bézier curve must be as small as possible.  
This new constraint explicitly requires the Bézier curve to stay near the circle—resulting in a better fit.  
The first constraint yields the parametric form of the Bézier curve:  
B(t) = (x,y), where:  
x(t) = 3*c*(1-t)^2*t + 3*(1-t)*t^2 + t^3  
y(t) = 3*c*t^2*(1-t) + 3*t*(1-t)^2 + (1-t)^3  
The radial distance from the arc to the Bézier curve is:  
d(t) = sqrt(x^2 + y^2) - 1  
![pic2](http://spencermortensen.com/articles/bezier-circle/.page/minimal.gif)  
The Bézier curve touches the right circular arc at its initial endpoint, then drifts outside the arc, inside, outside again, and finally returns to touch the arc at its endpoint.  
Figure 3. The radial distance from the arc to the ideal Bézier approximation.  
This radial distance function, d(t), has minima at t = 0, 1/2, 1, and maxima at t = 1/2 +- sqrt(12 - 20*c - 3*c^2)/(4 - 6*c).  
Because the Bézier curve is symmetric about t = 1/2, the two maxima have the same value. The radial deviation is minimized when the magnitude of this maximum is equal to the magnitude of the minimum at t = 1/2.  
This gives the ideal value for c:  
**c = 0.551915024494**  
The maximum radial drift is 0.019608% with this approximation. This is 28% better than the standard approximation.  
Here is the final result:  

Figure 4. The Bézier approximation is almost indistinguishable from a circle.  
Figure 4 was created using the Bézier curves:  
P_0 = (0,1), P_1 = (c,1), P_2 = (1,c), P_3 = (1,0)  
P_0 = (1,0), P_1 = (1,-c), P_2 = (c,-1), P_3 = (0,-1)  
P_0 = (0,-1), P_1 = (-c,-1), P_3 = (-1,-c), P_4 = (-1,0)  
P_0 = (-1,0), P_1 = (-1,c), P_2 = (-c,1), P_3 = (0,1)  
with **c = 0.551915024494**.  
