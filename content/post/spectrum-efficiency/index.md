---
title: How did I come up with the logo for Spectrum Efficiency?
description: Radio Frequency Spectrum Management unleashed by data automation.
slug: contact, spectrum management , data automation, R, Dashboard
date: 2022-03-06 00:00:00+0000
image: cover.png
categories:
    - r
    - methodology
    - visualisation
tags:
    - sinus
---

As always with anything you start with a blank canvas. In this document we will explore how to use some base function in `R` togheter with visualisation using `ggplot2` package.

# What is Spectum Efficiency

First I thought of what does Spectrum Efficiency sounds like. From there I thought of what we will talk about using this channel:

- somthing that has to do with radio frequency domain and spectrum allocation in general
- how to do it in an efficient manner, with as little waste both in time and value
- data is at the heart of this website so it must be embeded into the logo as well
# Radio Frequency
>Radio frequency (RF) is the oscillation rate of an alternating electric current or voltage or of a magnetic, electric or electromagnetic field or mechanical system in the frequency range from around 20 kHz to around 300 GHz. This is roughly between the upper limit of audio frequencies and the lower limit of infrared frequencies;these are the frequencies at which energy from an oscillating current can radiate off a conductor into space as radio waves. Different sources specify different upper and lower bounds for the frequency range (Wikipedia)

Aha, so it has to do with periods and ocilating things. The only representation I remeber vaguly resembling an S is a sinusoidal wave. So let's plot a `sin` of sequence of numbers and see what it looks like.

```r sinus
t=seq(0,6.3,0.1)
y=5*sin(t)
plot(t,y,type="l")
```

Right it seems that we are on the right path, but what about the __E__? I got an ideea. Let us use points for each of the extremities of E and lines for the body of the letter E, but reversed.

```r
## I would never do right assignment 
## but it does not look good on the 
## mobile file.
tibble(ID = c(1,2,3,4,5,6,7)
       ,X = c(0,0,3.125,3.125,3.125,6.25,6.25)
       ,Y = c(5,0,0,2.5,0,0,5),size = 5) -> df.points

knitr::kable(df.points) %>% 
  kableExtra::kable_styling(
    bootstrap_options = "striped",font_size = 12)
```

Now that we have the points let's see them on a graph. We use the `ggplot2`. To plot the points we will use `geom_point()` and for the line, you guesed it, we use `geom_line()`. The `geom` functions connects the observations in the order in which they appear in the data.

```r
# Selecte the data to plot

ggplot(data = df.points) +
# Select what type of geom to use
geom_line(
  aes(
    x = X,
    y = Y,
    color = "green",
    size = 5),
  show.legend = FALSE) +
  geom_point(
    aes(
      x = X,
      y = Y,
      color = "red",
      size = 9),
    show.legend = FALSE) +
labs(
  x = "",
  y = "",
  color = NULL,
  size = NULL,
  title = "The points show us the a pattern for the line to follow",
  subtitle = "The line is used to
  tie everything togheter.")
```

Now if we put it all togheter it starts to resemble the end product.

```r sinus with points


df.sin <- tibble(X = t,Y=y)

ggplot(
  data = df.sin,
  aes(x = X,y = Y)) +
  ## We inherit the aestetics from ggplot
  geom_line(
    aes(size = 5),
    show.legend = FALSE) +
  scale_x_continuous(
    breaks = c(1,2,3,4,5,6,
               7,8,9,10))+
  scale_y_continuous(
    breaks = c(-1,-2,-3,-4,
               -5,0,1,2,3,4,5))+
  # We plot the letter E
  geom_line(
    data = df.points,
    aes(x = X,y = Y,
        color = "green",
        size = 5),
    # We do not want to see the legend
    show.legend = FALSE) +
  geom_point(
    data = df.points,
    aes(x = X,y = Y,
        color = "red",
        size = 9),
    show.legend = FALSE) +
  ##
  ##business-science.io best online courses
  theme_tq() +
  scale_color_tq() +
labs(
  x ="",
  y ="",
  color = NULL,
  size = NULL,
  title = "This is how I came up with my log for Spectrum Efficiency",
  subtitle = "It is a revesed sinus wave and the letter E") 


```

In the end, this is what I presented to my brother in law who is an artist in Amsterdam. I wanted his view on how a logo should look. For not this is what we came up so far.