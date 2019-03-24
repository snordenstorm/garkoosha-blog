---
layout: post
tags: physics
date: 2019-03-23
title: The Free Fall of Vesna Vulović
published: true
---



On 26 January 1972 aircraft called McDonnell Douglas DC-9-32 was destroyed at the height 10,160 metres by a bomb placed by Croatian nationalists. Vesna (on the photo) spent 27 days in coma after the fall, but survived. At the moment, this is Guinness world record for free fall without a parachute. The second place survivor has fallen from the height of 5,000 metres.

<!--more-->

School physics protests against Vesna Vulović:

$$v = v_0 + at$$ $$x = x_0 + v_0 t + at^2/2$$

With acceleration $a$ being essentially gravitational acceleration $g$,  $x_0$ being $h$, and $v_0$ (the vertical component of plane speed) being zero, 

$$v = -gt$$ $$0 = h - gt^2/2 $$

Thus, $t = \sqrt{2h/g}$, and $v = - \sqrt{2gh}$. The minus sign should not confuse the reader — it indicates that coordinate $x$ ("height above the ground") decreases. Substituting 10,160 metres,

$$v = \sqrt{2 \cdot 9.8 \: \frac{\text{m}}{\text{s}^2} \cdot 10160 \: \text{m}} \approx 446 \: \frac{\text{m}}{\text{s}}$$

Well, it doesn't seem like a landing speed with which one can survive.

#### The drag force

The rules () are derived in an assumption that gravity is the only force in place. In fact, air resistance force plays crucial role for objects. It is directed opposite to the relative motion of .

While earlier we had $$ma = \sum\limits_{i} F_i = mg,$$ now $$ma = \sum\limits_{i} F_i = mg - kv^2$$
 where $k$ is air friction coefficient. Taking into account that body acceleration is the derivative of its velocity ($a = \dot v = dv/dt$), $$m \frac{dv}{dt} = mg - kv^2$$ $$\frac{mdv}{mg - kv^2} = dt$$

Integrating both parts, we obtain

$$ \frac{1}{2} \sqrt{\frac{m}{gk}}  \ln \left( \frac{\sqrt{mg/k} + v}{ \sqrt{mg/k} - v} \right) = t + C$$

Constant can be found from the initial condition: with $t=0$ starting velocity $v$ was also zero (free fall),  so
$$\frac{1}{2} \sqrt{\frac{m}{gk}}  \ln \left( \frac{\sqrt{mg/k} + 0}{ \sqrt{mg/k} - 0} \right) = 0 + C$$
$$\frac{1}{2} \sqrt{\frac{m}{gk}} \cdot \ln 1 = 0 + C$$
$$\frac{1}{2}\sqrt{\frac{m}{gk}} \cdot 0 = 0 + C$$
$$  0 = C$$

Thus, () can be rewritten as

$$ \frac{1}{2} \sqrt{\frac{m}{gk}}  \ln \left( \frac{\sqrt{mg/k} + v}{ \sqrt{mg/k} - v} \right) = t $$

While we have found the dependence $t(v)$, we've been seeking for something else: with $v(h)$ we could calculate the landing speed. 

After some arithmetics,

$$v = - \sqrt{\frac{mg}{k}} \left( 1 -    \frac{2}{ 1 + e^{2t \sqrt{\frac{gk}{m}}} } \right),$$

The velocity is bounded from above — see it? With $t \to \infty$ we see that the absolute value of our free falling body's velocity will never reach $\sqrt{\frac{mg}{k}}$.

Let's obtain the precise expression for $v_\text{landing} (h)$. Using hyperbolic functions, we rewrite ()
$$v = - \sqrt{\frac{mg}{k}} \tanh \left( t \sqrt{\frac{gk}{m}} \right)$$

and then enter another differential equation

$$\frac{dx}{dt} = - \sqrt{\frac{mg}{k}} \tanh \left( t \sqrt{\frac{gk}{m}} \right)$$

$$dx \frac{k}{m} = - \tanh \left( t \sqrt{\frac{gk}{m}} \right) dt \sqrt{\frac{gk}{m}}$$

$$x \frac{k}{m} = - \ln \cosh \left( t \sqrt{\frac{gk}{m}} \right)  + C$$

For $t = 0$ the height $x$ was equal to $h$, so $$h \frac{k}{m} = C$$ ($\cosh 0 = 1, \ln \cosh 0 = 0$).

Our goal remains the same: the dependence $v(h)$. Keeping going...

$$e^{(h-x) \frac{k}{m}} = \cosh \left( t \sqrt{\frac{gk}{m}} \right)  $$

$$e^{t \sqrt{\frac{gk}{m}}} = e^{(h-x) \frac{k}{m}} + \sqrt{e^{2(h-x) \frac{k}{m}} - 1}$$ 

$$e^{2t \sqrt{\frac{gk}{m}}} = \left( e^{(h-x) \frac{k}{m}} + \sqrt{e^{2(h-x) \frac{k}{m}} - 1} \right)^2$$

$$v = - \sqrt{\frac{mg}{k}} \left( 1 -    \frac{2}{ 1 + \left( e^{(h-x) \frac{k}{m}} + \sqrt{e^{2(h-x) \frac{k}{m}} - 1} \right)^2 } \right)$$

$$v = - \sqrt{\frac{mg}{k}} \left( 1 -    \frac{1}{ e^{2(h-x) \frac{k}{m}}  +  e^{(h-x) \frac{k}{m}} \sqrt{e^{2(h-x) \frac{k}{m}} - 1}  } \right)$$

On the ground, $x=0$, so for the landing speed

$$v_\text{landing} = - \sqrt{\frac{mg}{k}} \left( 1 -    \frac{1}{ e^{\frac{2hk}{m}}  +  e^{\frac{hk}{m}} \sqrt{e^{\frac{2hk}{m}} - 1}  } \right)$$

Once again, the velocity is limited (cannot reach $\sqrt{mg/k}$, but gets close to it fast).

