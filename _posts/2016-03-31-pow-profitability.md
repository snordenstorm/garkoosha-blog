---
layout: post
tags: pow
date: 2016-03-31
title: On PoW mining profitability
published: true
---

<!--Ethereum hashing algorithm (dagger-hashimoto) is ASIC-resistant by design: it requires at least 1 Gb of RAM, and the requirements grow with the growth of Ethereum mainnet chain. Only general-purpose hardware (CPU/GPU) suits for this mining algorithm, with GPU being clearly the most efficient.-->

Creating a coin, you will probably give its initial distribution a think. 

There are three *fair* ways to conduct initial coin distribution. First fair way is to organize a free-to-play competition, participating in which, people could earn the coins. (This is what is called proof-of-work mining, or PoW mining.) Second fair way is to offer anyone to buy the coins. (This is called crowdsale.) Third fair way is to offer anyone to burn their money, typically by sending their bitcoin to the address it would take an expected time of several Universe existence times to brute-force the private key. (This is called proof-of-burn.) A giveaway without explicit rules provides us an example of an *unfair* initial coin distribution, since, in this case, monetary reward is not proportional to the amount of resource sacrificed.

In this post, we will briefly discuss the first fair way of initial coin distribution — PoW mining.

<!--more-->



This free-to-play competition is, in almost all cases, competition in computation. People buy and setup the hardware, typically GPUs or ASICs, depending on currency they choose to mine. For the sake of generality, we call this currency XYZ.

Let $h$ be the hashing power of our miner [hash/s], $N$ be the quantity of rigs bought. Clearly, together all rigs are having hashing power of $Nh$ hash/s.



The share under control of such a miner is $\frac{Nh}{H + Nh},$ where $H$ [hash/s] is total network hashrate before she turned her rigs on. Daily revenue is $\frac{Nhap}{H + Nh}$, where $a$ is the daily average amount of currency mined by the network (piecewise-constant; in most protocols, [it is constant for years](https://en.bitcoin.it/wiki/Controlled_supply)), and $p$ is XYZ/USD exchange rate (the dollar price of 1 XYZ coin). Daily costs are $24ewN$, where $e$ is dollar price of 1 kilowatt-hour (varies from region to region), and $w$ is electric power consumption of the GPU in kilowatts.

Thus, 

$$ \label{daily} \text{daily farm revenue} = N \left( \frac{hap}{H + Nh} - 24ew \right)$$

To calculate monthly farm profit, one might want to multiply this expression by 30 (or 31, religion-dependent). That would lead to the incorrect result: average total network hashrate $H$ varies in time, and varies significantly. What was network hashrate a week ago, may be pretty far from a network hashrate now.

Parameters $H$, $p$ are (un)predictable and do not depend on the miner. Unlike them, parameters $e$, $w$, $h$, $c$ are known at the very start (with one of our goals being to choose rigs and mining farm location so that $h$ is as high as possible, and $e$, $w$, $c$ are as low as possible).

Typically, network hashrate grows in time, but that's not the rule, and drawdowns also happen. Network hashrate heavily depends on the coin price. If price skyrockets, mining gets very profitable, so more people buy the rigs and mining difficulty gets higher into the cloud. If price diminishes or in case of hot weather, miners may switch off some of their mining rigs.

To come up with a correct formula for monthly farm profit, you have to sum up the daily profits calculated with correct changing values of $H$ — essentially integrating the expression (\ref{daily}):

$$ \label{monthly} \text{monthly farm revenue} = N \int\limits_{t_{\text{month start}}}^{t_{\text{month end}}} dt\left( \frac{hap}{H(t) + Nh} - 24ew \right) $$

As we pointed out earlier, $H$ is more likely to grow than decline. Historical data says so. 



#### Gross profit of our farm 

To tell if this mining venture is financially sound, we shall, of course, take into account that these rigs have their cost. Let $c$ be the dollar price of one mining rig, let $s$ be its shipping cost, and let $o$ be the cost of supplementary hardware or other expense one rig creates (the overhead cost). 

This turns (\ref{monthly}) into 

$$ \label{total} \text{total farm profit} = - N (c+s+o) + N \int\limits_{t_{\text{start}}}^{t_{\text{off}}} dt\left( \frac{hap}{H(t) + Nh} - 24ew \right) $$

One can remark here: coin price $p$ changes with the time just as hashrate $H$ does, why doesn't the formula reflect it? The answer is, this dependence matters only if we sell the mined coins right after they are mined, if there is a continuous process of "selling" running in parallel to the process of "mining". Typically the situation is different and coins are sold "in portions"; $p$ is the exchange rate at the day coin is sold.

Starting from here, one can approximate the next year's $H(t)$ by linear, quadratic or by exponential function, making profitability plan:

$$H(t) = H_{\text{start}} + k (t - t_{\text{start}})$$

$$H(t) = H_{\text{start}} + k (t - t_{\text{start}}) + m (t - t_{\text{start}})^2$$

$$H(t) = H_{\text{start}} \cdot  e^{\alpha (t - t_{\text{start}})}$$

The art of being an entrepreneur comprises the ability to guess the correct form of the function, and to estimate the coefficients $k$, $m$, $\alpha$ well. One may find recent historical data (last month, last quarter, last year) helpful for these estimations. 

Our role here is to perform the math and calculate the profit for each of the three extrapolations: linear, quadratic, and exponential one. To simplify the calculations, we would like to point out that in most cases $Nh \ll H(t)$, so $Nh$ in denominator can be safely neglected, turning the r.h.s. of (\ref{total}) into

$$\text{total farm profit} = - N (c+s+o) + N \int\limits_{t_{\text{start}}}^{t_{\text{off}}} dt\left( \frac{hap}{H(t)} - 24ew \right)  =  - N (c+s+o)  - 24eNw (t_{\text{off}} - t_{\text{start}})+ Nhap \int\limits_{t_{\text{start}}}^{t_{\text{off}}} \frac{dt}{H(t)}  $$

Consider the integral

$$  I = \int\limits_{t_{\text{start}}}^{t_{\text{off}}} \frac{dt}{H(t) } $$

In linear extrapolation case, it is not hard to check that

$$  I_{\text{linear}} = \int\limits_{t_{\text{start}}}^{t_{\text{off}}} \frac{dt}{H_{\text{start}} + k (t - t_{\text{start}}) }   = \frac{1}{k} \ln \left(1 + \frac{k (t_{\text{off}} - t_{\text{start}})}{H_{\text{start}}} \right)  $$

For quadratic extrapolation,

$$  I_{\text{quadratic}} = \int\limits_{t_{\text{start}}}^{t_{\text{off}}} \frac{dt}{H_{\text{start}} + k (t - t_{\text{start}})  + m (t - t_{\text{start}})^2}   =  \frac{2}{\sqrt{4m H_{\text{start}} - k^2}} \left( \arctan \frac{2m (t_{\text{off}} - t_{\text{start}}) + k}{\sqrt{4m H_{\text{start}} - k^2}} - \arctan \frac{ k}{\sqrt{4m H_{\text{start}} - k^2}} \right) $$

In exponential case,

$$  I_{\text{exp}} = \int\limits_{t_{\text{start}}}^{t_{\text{off}}} \frac{dt}{H_{\text{start}} \cdot  e^{\alpha (t - t_{\text{start}})} }   = \frac{1 - e^{-\alpha (t_{\text{off}} - t_{\text{start}})}}{\alpha H_{\text{start}}} $$

You substitute one of the three expressions for the integral into (\ref{total}), and this is it. Apart from choosing the most accurate approximation with accurate coefficients ($k$, $m$, $\alpha$), the assessment of unit shipping cost $s$ and overhead cost $o$ is also critical for the success of the venture.


#### When it gets unprofitable

The time $t_{\text{off}}$ is not infinity. It may happen that some day, with the growth of the network hashrate, electricity costs get bigger than revenue associated with mining. This is the day the rigs become obsolete, and mining with them should be stopped by that point. It gets economically sound to switch them off.

When this happens, integrand in (\ref{total}) becomes zero: 

$$ \frac{hap}{H_{\text{critical}}} - 24ew = 0$$

$$  H_{\text{critical}} = \frac{hap}{24ew} $$

Having this, and using linear, quadratic or exponential approximations, you may estimate the LTV of your rigs.




#### Can I profit well on mining?


In 2016 mining is hard business with very unclear profit perspectives. Those who decided to enter this business:

1. find a place with industrial electricity that is as cheap as possible (e.g. nearby powerplant) 
2. rent an abandoned warehouse 
3. buy a huge amount of specific (ASICs) or non-specific (GPUs) hardware 
4. configure them and turn on


The perspectives are obscure. By March 2016 Bitcoin total hashing power [fluctuates around](https://blockchain.info/charts/hash-rate) $1.2 \cdot 10^{18}$ hashes per second. On average, 3600 bitcoins are mined every day; if an enterpreneur wants to earn 1 BTC a day by mining, his hashing power $h$ should constitute roughly $1/3600$ of total network hashrate. Let's write it in equation: $$\frac{h}{1.2 \cdot 10^{18} + h} = \frac{1}{3600},$$ where $h$ is hashing power to be acquired (bought or produced).

It's pretty easy to solve this equation. Since $1/3600$ is small fraction, $h \ll 1.2 \cdot 10^{18}$ holds, so $$\frac{h}{1.2 \cdot 10^{18} + h} \approx \frac{h}{1.2 \cdot 10^{18}}.$$ Thus  

$$h = 1.2 \cdot 10^{18} \cdot \frac{1}{3600} = 3.33 \cdot 10^{14} \frac{\text{hash}}{\text{s}} = 333 \frac{\text{Thash}}{\text{s}}$$

Thus, for our purpose (to earn 1 BTC/day by mining) we should buy sha256-hashing hardware that can calculate 333 Thash/s.

By March 2016 AntMiner S5+ is the rig with highest hashrate. Its hashing power is 7.7 Thash/s and it can be purchased for \$ 2307 (shipping cost excluded). To achieve 333 Thash/s, one should buy 43 of them, with expenses totalling to $100,000. Earning 1 BTC per day (w.r.t. March 2016 prices, 1 BTC = \$ 415), we reach breakeven point by day 239. By this day, total network hashrate can grow twice, thrice and to the moon; in reality, our revenue will become lower every day, and our investments will not always break even. In this reasoning, we didn't take into account electricity, staff and warehouse rent expenses.

Moreover, in June 2016 the next halving will happen --- according to Bitcoin protocol, every 210000 blocks block reward [becomes twice lower](https://en.bitcoin.it/wiki/Controlled_supply). In terms of bitcoin, daily mining profit will fall twice. However, this does not mean necessarily losses --- if BTC/USD exchange rate grows more than twice at the time, miners wouldn't earn less. As you see, mining profitability highly depends on bitcoin exchange rate, since miners each in bitcoin and spend (buy rigs, pay for electricity) in fiat currencies.

Mining ecosystem resembles of California gold rush at the moment --- by that time, those who earned more were device manufacturers. When first ASICs started shipping, some buyers posted on Bitcointalk evidences of manufacturing company mining on those devices prior to shipping.


