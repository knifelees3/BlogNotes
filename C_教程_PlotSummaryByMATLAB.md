---
title: MATLAB plot summary
date: 2019-04-06 19:15:50
tags:
- MATLAB
categories: 
- 技术
---

create time: 2019 03 20
## update log:
* 2019 04 06 
add the 1d plot code
# Notes of plotting in MATLAB
MATLAB is a power software in scientific calculations and its plot ability is also useful. I want to summarize the most frequently used MATLAB code accoring to my usage.
## Basic one dimensional plot

### plot multi lines in the same figures
The first code is how we plot multilines in the same plot. I want to add some extra settings in this code for the default settings are not so beautiful. The following is the plot of different functions:

```
numx=200;
x=linspace(-1,10,numx);
y1=exp(x);
y2=sin(x)+exp(-x);
y3=x.^3+x.^2+1;
y4=sin(x).*exp(-x);
%%
figure(1)
plot(x,y1,'linewidth',2)
hold on
plot(x,y2,'linewidth',2)
hold on
plot(x,y3,'linewidth',2)
hold on
plot(x,y4,'linewidth',2)
hold on
set(gca,'linewidth',2,'fontsize',15)
xlabel('x','fontname','times newroman','fontsize',15)
ylabel('y','fontname','times newroman','fontsize',15)
%xlim([0,10])
ylim([-5,10])
legend({'lin1','lin2','lin3','lin4'},'fontname','times newroman','fontsize'...
    ,15,'Location','northwest','Orientation','horizontal')

```
In above figures I redefined the linewidth of the lines and ticks,changed the fontsize of legend,label etc.
![Basic 1d plot](https://raw.githubusercontent.com/knifelees3/my_pictures/master/20190406_MATLAB_PLOT/example_01_1d.png)

### Plot different lines by using different y axis
In some cases we need to plot different things in the smae plot but their number and meanings are different and are not suitable compared directly. We may need the double yy plot.
```
x = linspace(0, 10);
y1 = sin(3*x);
y2 = sin(3*x) .* exp(0.5*x);

figure(1)
subplot(2,1,1)
yyaxis left;
plot(x,y1,'Linewidth',1);
title('yyaxis');
xlabel('X-axis','fontname','times newroman','fontsize',15);
ylabel('left Y-axis','fontname','times newroman','fontsize',15);

yyaxis right;
plot(x,y2,'Linewidth',1);
ylim([-150,150]); 
ylabel('right Y-axis','fontname','times newroman','fontsize',15); 
%set(gca,'linewidth',1.5,'fontsize',15)
% plotyy
subplot(2,1,2)
x = 0:0.01:20;
y1 = 200*exp(-0.05*x).*sin(x);
y2 = 0.8*exp(-0.5*x).*sin(10*x);
[hAx, hLine1, hLine2] = plotyy(x,y1, x,y2);

title('plot yy');
xlabel('Time (\musec)');

ylabel(hAx(1), 'Slow Decay'); % left y-axis
ylabel(hAx(2), 'Fast Decay'); % right y-axis
```
![plot by using different yaxis](https://raw.githubusercontent.com/knifelees3/my_pictures/master/20190406_MATLAB_PLOT/example_02_1d.png)

### Plot the interpolation lines with its origin data
We sometimes need to draw some discrete data into a line. In order to look good, we need a smooth curve. In this case, we need to use interpolation. We then give an example to show how to plot . There are two different methods: "plotyy" and "yyaxis"
```
Nx=12;
power=zeros(Nx,2);
power(:,1)=linspace(1,10,Nx);
power(:,2)=[3,6,4,2,1,5,8,10,4,3,2,9];
xmin=power(1,1);
xmax=power(Nx,1);
deltax=(xmax-xmin)/(Nx-1)/10;
xi=xmin:deltax:xmax;
yi=interp1(power(:,1),power(:,2),xi,'spline');

figure(1)
plot(power(:,1),power(:,2),'>',xi,yi,'Linewidth',2);
%axis([4.5 22.5 10.2 10.7])
xlabel('x','fontname','times newroman','fontsize',15)
ylabel('y','fontname','times newroman','fontsize',15)
legend({'origin','interp'},'fontname','times newroman','fontsize'...
    ,15,'Location','northwest','Orientation','horizontal')
grid
set(gca,'linewidth',1.5,'fontsize',15)
```
![Plot from discrete date and do Interpolation](https://raw.githubusercontent.com/knifelees3/my_pictures/master/20190406_MATLAB_PLOT/example_03_1d.png)
## Basic two dimensioal map
### Contour

### Surf

### Mesh

### pcolor
