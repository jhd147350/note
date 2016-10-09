#Approximate a circle with cubic Bézier curves  
>A good cubic Bézier approximation to a circular arc is:  
P0 = (0,1), P1 = (c,1), P2 = (1,c), P3 = (1,0)  
c = 0.551915024494  
This yields an arc on the unit circle centered about the origin, starting at P0 and and ending at P3, with the least amount of radial drift.
