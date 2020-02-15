# How To Embed Animation Into Jupyter Notebook



Recently I struggled to choose the right way to write python. I'm not willing to use bloatware such as spyder to write. Since I want to feel very free when I want to start to write. This could be done via text eidter such as sublime text or vs code. However, my another demand is to write the note and code in the same file. This demand could be best solved via jupyter notebook when you want to solve something and show how you solve it. 



I have tested the way of animating the plot by using the package Matplotlib. A more natural idea is that can the animated plot be shown in jupyter notebook. After searching in the web I know this couldn't be solved directly. Different people offer different solutions. I choose the most simple and direct solution (at least in my mind). This is the [solution](https://www.numfys.net/howto/animations/).



Here is a simple examle from this [web](https://www.numfys.net/howto/animations/)



```python

from matplotlib import animation

from IPython.display import HTML



# First set up the figure, the axis, and the plot element we want to animate

fig = plt.figure()

ax = plt.axes(xlim=(0, 1), ylim=(-6, 10))

line, = ax.plot([], [], lw=1)



# Initialization function: plot the background of each frame

def init():

    line.set_data([], [])

    return line,



# Animation function which updates figure data.  This is called sequentially

def animate(i):

    line.set_data(x, u[i,:])

    return line,



# Call the animator.  blit=True means only re-draw the parts that have changed.

anim = animation.FuncAnimation(fig, animate, init_func=init,

                               frames=Nt, interval=20, blit=True)



plt.close(anim._fig)



# Call function to display the animation

HTML(anim.to_html5_video())

```



I want tp try this method and I hope to use one of my original program which shows the difference between the actual case and harmonic oscillator approximation when [a sphere slides down from a semi-circle](https://knifelees3.github.io/2019/07/23/A_En_Python_PlotStudy1_SemiCircle_OscilatorApprox/). I want show show the plot displyed in the jupyter notebook and can be controled via some buttons. This can be realized by directly adding two extra lines into the original program.  To show the animation like a video in the jupyter notebook, 



```python

from IPython.display import HTML

HTML(anim.to_html5_video())

```



Then you will see the following animated video in the explorer

![The animated plot](https://raw.githubusercontent.com/knifelees3/my_pictures/master/picgoup/20200202_HarmonicJupyterBook.gif)



If you want to control the animated plot, you could type



```python

HTML(anim.to_jshtml())

```



then you can control the animated plot by hand.



![Interactive plot](https://raw.githubusercontent.com/knifelees3/my_pictures/master/picgoup/20200202_HarmonicJupyterBookInterac.gif)

