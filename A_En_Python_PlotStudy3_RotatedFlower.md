# A rotated flower plotted via python (animated)



**All the python study code can be found in my [own repository](https://github.com/knifelees3/Study_Python).**



As a study of Python data visualization, I plot a 3D follower and let it rotated horizontally. The packages I used are



```python

import subprocess

import numpy as np

from matplotlib import pyplot as plt

from matplotlib import animation

from mpl_toolkits.mplot3d import Axes3D

from matplotlib import cm

from matplotlib.ticker import LinearLocator

```



The follower is defined via the following data



```python

[x, t] = np.meshgrid(np.array(range(25))/24.0,

                     np.arange(0, 575.5, 0.5)/575*17*np.pi-2*np.pi)



p = (np.pi/2)*np.exp(-t/(8*np.pi))



u = 1-(1-np.mod(3.6*t, 2*np.pi)/np.pi)**4/2



y = 2*(x**2-x)**2*np.sin(p)



r = u*(x*np.sin(p)+y*np.cos(p))

```

and the init function is as follows



```python

def init():



    surf = ax.plot_surface(r*np.cos(t), r*np.sin(t), u*(x*np.cos(p)-y*np.sin(p)),

                           rstride=1, cstride=1, cmap=cm.gist_rainbow_r, linewidth=0, antialiased=True)

    plt.axis('off')

    return fig,

```



An animate function



```python

def animate(i):

    # azimuth angle : 0 deg to 360 deg

    ax.view_init(elev=10, azim=i*4)

    return fig,



```



plot and save

```python

n = 'rotate_azimuth_angle_3d_flower'

# ani.save(fn+'.mp4',writer='ffmpeg',fps=1000/50)

ani.save(fn+'.gif', writer='imagemagick', fps=1000/50)



cmd = 'magick convert %s.gif -fuzz 5%% -layers Optimize %s_r.gif' % (fn, fn)

subprocess.check_output(cmd)





plt.rcParams['animation.html'] = 'html5'

ani

```



The generated flowers are as follows

![Flowers](https://raw.githubusercontent.com/knifelees3/my_pictures/master/picgoup/rotate_azimuth_angle_3d_flower_r.gif)



