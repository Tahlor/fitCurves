fitCurves
=========

Python implementation of Philip J. Schneider's "Algorithm for Automatically Fitting Digitized Curves" from the book "Graphics Gems"

Fit one or more cubic Bezier curves to a polyline.

This is a python implementation of Philip J. Schneider's C code. The original C code is available on http://graphicsgems.org/ as well as in https://github.com/erich666/GraphicsGems

The python implementation uses NumPy

demo.py is a example gui application using Tkinter.

![demo](https://github.com/volkerp/fitCurves/raw/master/demo_screenshot.png "demo.py")


%reload_ext autoreload
%autoreload 2

import fitCurves 
import numpy as np
from matplotlib import pyplot as plt

a = np.array([1.0,2,3,4,5,6,7,8,8,7,6,5,4,3,2,1]).reshape(-1,2)
cc = fitCurves.main.fitCurve(a, maxError=20)
print(a)
for c in cc:
    print(c) # list of beziers, [start, control1, control2, end]
    x,y = fitCurves.bezier.bezier_curve(c, 100)

    plt.plot(x,y)
plt.show()

old_points = a
new_points = fitCurves.main.smooth(old_points, 20)
plt.plot(old_points[:,0],old_points[:,1])
plt.plot(new_points[:,0],new_points[:,1])