---
layout: article
title: How to Create Black Graphs in MatLab
tags: MatLab Script
---

Sometimes it is useful to change the whole appearance of a graph because of presenting purposes or maybe just because it looks cool.

I mostly use two colours: one for the background and another one for the accents of what should be seen in front of the background.

Firstly we should get the pointers to the figure and the axis we are working with.
For example we can get the pointers to the current figure, axis and title.
{% highlight MatLab %}
fig = gcf;
ax = gca;
t = title('The Title');
{% endhighlight %}

For the background of the whole figure we need to set the Color attribute.
{% highlight MatLab %}
set(gcf, 'Color', [0.1 0.1 0.1]);
{% endhighlight %}

For the background of the axis and the colour of lines the commands are:

{% highlight MatLab %}
set(ax, 'Color', [0.1 0.1 0.1]);
ax.XAxis.Color = [0.8 0.8 0.8];
ax.YAxis.Color = [0.8 0.8 0.8];
{% endhighlight %}

The first line changed the background colour inside the axis while the last two lines change the colour of the axes themselves. Another thing one should do is to update the colour of the title which by the same method con become:

{% highlight MatLab %}
set(t, 'Color', [0.8 0.8 0.8]);
{% endhighlight %}

To make it easier to use one can encode it in an handy MatLab function. To see this function and other ones I regularly use one can check my GitHub Repo with MatLab functions.
