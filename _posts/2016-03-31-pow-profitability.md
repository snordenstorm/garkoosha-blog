---
layout: post
tags: pow
date: 2018-03-31
title: Ethereum mining profitability
published: true
---

Ethereum hashing algorithm (dagger-hashimoto) is ASIC-resistant by design: it requires at least 1 Gb of RAM, and the requirements grow with the growth of Ethereum mainnet chain. Only general-purpose hardware (CPU/GPU) suits for this mining algorithm, with GPU being clearly the most efficient.

<!--more-->

So we need to buy some GPUs to start off. Let $h$ be the hashing power of the chosen GPU (Mhash/s), $N$ be the quantity of GPU bought. Clearly, together all GPUs are having hashing power of $Nh$ Mhash/s.

Then the share under our control is $\frac{Nh}{H + Nh},$ where $H$ is total network hashrate (in Mhash/s). Daily revenue is $\frac{Nhap}{H + Nh}$, where $a$ is the daily average amount of ether mined by the network, $p$ is dollar price of 1 ETH. Daily costs are $24ewN$, where $e$ is dollar price of 1 kilowatt-hour, $w$ is electric power consumption of the GPU.

Thus, $$\text{profit per day} = N \left( \frac{hap}{H + Nh} - 24ew \right).$$

#### Gross profit of our farm 

Let $c$ be the dollar price of GPU. In addition, imagine total network hashrate $H$ is constant with the time (this is very far from being correct in most situations). In that occasion, the daily earning will be same every day, thus $$\text{net profit} (t) = Nt \left( \frac{hap}{H + Nh} - 24ew \right) - Nc,$$ where $t$ is time (in days) since we turned on our mining rigs. \boxed{Shipping costs are not considered in this research.}

In realistic case of non-constant total network hashrate $H(t)$ the following is correct: $$\text{profit} (t) = N \int\limits_{t_0}^{t_{\text{end}}} dt\left( \frac{hap}{H(t) + Nh} - 24ew \right) - Nc,$$ where $t_{\text{end}}$ is the day when it is economically rational to turn mining rigs off (mining profit becomes lower than electricity cost).

Let's start with linear approximation for $H(t)$: $H(t) = H_0 + k (t - t_0)$, $k \neq 0$. Поскольку в большинстве случаев $Nh \ll H(t)$, отбросим $Nh$ и получим $$\text{net profit} = N \int\limits_{t_0}^{t_{\text{end}}} dt\left( \frac{hap}{H_0 + k (t - t_0)} - 24ew \right) - Nc =$$ $$= N \left( \int\limits_{t_0}^{t_{\text{end}}}  hap \frac{dt}{H_0 + k (t - t_0)} - 24ew (t_{\text{end}} - t_0) - c \right) = N \left(  \frac{hap}{k} \ln \left(H_0 + k (t - t_0)\right)\Bigg|_{t_0}^{t_{\text{end}}} - 24ew (t_{\text{end}} - t_0) - c \right) = $$ $$= N \left( \frac{hap}{k} \ln \frac{H_0 + k (t_{\text{end}} - t_0)}{H_0} - 24ew (t_{\text{end}} - t_0) - c \right),$$

where $t_{\text{end}}$ is, again, the day when it is economically rational to turn mining rigs off (mining profit becomes lower than electricity cost): $$\frac{hap}{H_0 + k (t_{\text{end}} - t_0)} = 24ew$$ $$\frac{hap}{24ew} - H_0 = k (t_{\text{end}} - t_0)$$ $$t_{\text{end}} = t_0 + \frac{hap}{24ewk} - \frac{H_0}{k}$$

Substituting $t_{\text{end}}$ in (), we obtain $$ \text{net profit} = N \left( \frac{hap}{k} \ln \frac{hap}{24ew H_0} - 24ew \left(\frac{hap}{24ewk} - \frac{H_0}{k}\right) - c \right) = $$ $$= N \left( \frac{hap}{k} \ln \frac{hap}{24ew H_0} - \frac{hap - 24ew H_0}{k} - c \right)$$ (from above it is clear that $hap > 24ew H_0$).

#### Profitability threshold for the GPU

Clearly, if the value of $k$ is very big positive, mining is unprofitable (and if $k$ is negative or slightly positive, it is profitable). Before the start, it is always good to compare our guess for $k$ with profitability threshold.

$$\text{total profit} > 0$$ $$N \left( \frac{hap}{k} \ln \frac{hap}{24ew H_0} - \frac{hap - 24ew H_0}{k} - c \right) > 0$$ $$ hap \ln \frac{hap}{24ew H_0} - \left(hap - 24ew H_0\right) > ck $$ $$k < \frac{hap}{c} \ln \frac{hap}{24ew H_0} - \frac{hap - 24ew H_0}{c}$$

#### GPU breakeven day

This is breakeven day $t_{\text{be}}$ calculation. $$0 = N \int\limits_{t_0}^{t_{\text{be}}} dt\left( \frac{hap}{H_0 + k (t - t_0)} - 24ew \right) - Nc $$ $$c = \int\limits_{t_0}^{t_{\text{be}}} dt\left( \frac{hap}{H_0 + k (t - t_0)} - 24ew \right) = $$ $$=  \int\limits_{t_0}^{t_{\text{be}}}  hap \frac{dt}{H_0 + k (t - t_0)} - 24ew (t_{\text{be}} - t_0) =  \frac{hap}{k} \ln \left(H_0 + k (t - t_0)\right)\Bigg|_{t_0}^{t_{\text{be}}} - 24ew (t_{\text{be}} - t_0)  = $$ $$=  \frac{hap}{k} \ln \frac{H_0 + k (t_{\text{be}} - t_0)}{H_0} - 24ew (t_{\text{be}} - t_0) $$

At the moment, total network hashrate is $H_0 = 1661000$ Mhash/s, $k = 27000$, $t = (t_{\text{be}} - t_0)$ is the mining rigs worktime (in days). Поэтому логарифм берётся от величины $$\frac{1661 + 27t}{1661} \approx 1 + 0.016t$$ За 61.5 дней $\ln(1+x)$ превратится в $\ln 2$. Вообще, ряд от логарифма сходится очень медленно ($\ln (1+x)\Bigg|_{x=1} = \ln 2 \approx 0.693$, $x - x^2/2\Bigg|_{x=1} = 1 - 1/2 = 0.5$), поэтому, если его обрубить (воспользоваться рядом Тейлора), ошибка будет большой. Ещё раз: к сожалению, ряд Тейлора даст слишком большую ошибку, поэтому уравнение это придётся решать без упрощений, т.е. численно.

Parameters $H$, $p$ are (un)predictable and do not depend on the miner. Unlike them, parameters $e$, $w$, $h$, $c$ are known at the very start (with one of our goals being to choose GPUs and mining farm location so that $h$ is as high as possible, and $e$, $w$, $c$ are as low as possible).

Regarding $a$, $a = 20 \cdot 60 \cdot 24 = 28800$ must be true, but current value is $31000$. And this is the value we'll be using: $a = 31000$.

The parameter $e$ varies from region to region. 

Let us provide estimate for $k$. For 29 February 2016 we have $H = 868$ Ghash/s, for 30 March 2016 $H = 1661$ Ghash/s. Average daily growth for this month was $$\frac{1661 - 868}{30} \approx 26.433 \:\: \frac{\text{Ghash}}{\text{s}},$$ thus, $k$ turned out to be equal to $26433$. For convenience, we will round it to are slightly higher value: $k = 27000$.

Total network hashrate constantly grows, ether dollar price $p$ is highly unpredictable. All the following computations are done w.r.t. assumption that ether price will fluctuate around $p = 12$, and hashrate will grow with same rate as we saw last month ($k = 27000$).


\paragraph{\textcolor{RoyalBlue}{Radeon HD 7990}}
 
\subparagraph{Случай неизменного хэшрейта} In assumption of constant total network hashrate and constant ether price:

This GPU has $h = 50$, $w = 0.375$, $c = 532$. Подставляя, имеем: $$\text{profit} (t) = Nt \left( \frac{hap}{H + Nh} - 24ew \right) - Nc \approx Nt \left( \frac{hap}{H} - 24ew \right) - Nc = $$ $$= Nt \left( \frac{50 \cdot 31000 \cdot 12}{1661000} - 24 \cdot 0.075 \cdot 0.375 \right) - 532 N \approx 10.523 Nt - 532 N$$ Точка выхода на окупаемость $$t = \frac{532}{10.523} \approx 50.556 \:\:\text{days}$$ 

\subparagraph{Как должен расти хэшрейт, чтобы окупить вложения?}

Неравенство на $k$ $$k < \frac{hap}{c} \ln \frac{hap}{24ew H_0} - \frac{hap - 24ew H_0}{c} =$$ $$= \frac{50 \cdot 31000 \cdot 12}{532} \ln \frac{50 \cdot 31000 \cdot 12}{24\cdot 0.075 \cdot 0.375 \cdot 1661000} -$$ $$- \frac{50 \cdot 31000 \cdot 12 - 24\cdot 0.075 \cdot 0.375 \cdot 1661000}{532} = 65347$$

Таким образом, $k$ должно быть меньше, чем $65347$ (Mhash/s)/day. Это означает, что для окупаемости хэшрейт должен расти меньше, чем на 65 Ghash/s в день.



\subparagraph{One GPU profit ($k = 27000$)}

$$ \text{net profit} = N \left( \frac{hap}{k} \ln \frac{hap}{24ew H_0} - \frac{hap - 24ew H_0}{k} - c \right) = $$ $$= N \left( \frac{50 \cdot 31000 \cdot 12}{27000} \ln \frac{50 \cdot 31000 \cdot 12}{24 \cdot 0.075 \cdot 0.375 \cdot 1661000} - \frac{50 \cdot 31000 \cdot 12 - 24\cdot 0.075 \cdot 0.375 \cdot 1661000}{27000} - 532 \right) $$ $$= 755.576 N$$

Чистая прибыль с одной видеокарты составит \$755.

\subparagraph{Сроки окупаемости при текущем $k = 27000$}

$$t_{\text{be}} - t_0 = \frac{c}{\frac{hap}{H_0} - 24ew}$$

$$ с = \frac{hap}{k} \ln \frac{H_0 + k (t_{\text{be}} - t_0)}{H_0} - 24ew (t_{\text{be}} - t_0) $$ $$ 532 = \frac{50 \cdot 31000 \cdot 12}{27000} \ln \frac{1661000 + 27000 t}{1661000} - 24\cdot 0.075 \cdot 0.375 \cdot t, $$ откуда $t$ можно найти численно. Если проделать это, получится $t \approx 82.918 \:\:\text{days}$, т.е. видеокарта окупится на 83-й день. 


\paragraph{\textcolor{RoyalBlue}{Radeon HD 7970}} 

\subparagraph{Случай неизменного хэшрейта} Для этой видеокарты $h = 22$, $w = 0.25$, $c = 150$. Подставляя, имеем: $$\text{profit} (t) = Nt \left( \frac{hap}{H + Nh} - 24ew \right) - Nc \approx Nt \left( \frac{hap}{H} - 24ew \right) - Nc = $$ $$= Nt \left( \frac{22 \cdot 31000 \cdot 12}{1661000} - 24 \cdot 0.075 \cdot 0.25 \right) - 150N = 4.477 Nt - 150N$$ Точка выхода на окупаемость $$t = \frac{150}{4.477} \approx 33.505 \:\:\text{days}$$ 

\subparagraph{Как должен расти хэшрейт, чтобы окупить вложения?}

Неравенство на $k$ $$k < \frac{hap}{c} \ln \frac{hap}{24ew H_0} - \frac{hap - 24ew H_0}{c} =$$ $$= \frac{22 \cdot 31000 \cdot 12}{150} \ln \frac{22 \cdot 31000 \cdot 12}{24\cdot 0.075 \cdot 0.25 \cdot 1661000} -$$ $$- \frac{22 \cdot 31000 \cdot 12 - 24\cdot 0.075 \cdot 0.25 \cdot 1661000}{150} = 81000$$

Таким образом, $k$ должно быть меньше, чем $81000$ (Mhash/s)/day. Это означает, что для окупаемости хэшрейт должен расти меньше, чем на 81 Ghash/s в день.


\subparagraph{Чему будет равна прибыль с одной видеокарты при текущем $k = 27000$?} 

$$ \text{net profit} = N \left( \frac{hap}{k} \ln \frac{hap}{24ew H_0} - \frac{hap - 24ew H_0}{k} - c \right) = $$ $$= N \left( \frac{22 \cdot 31000 \cdot 12}{27000} \ln \frac{22 \cdot 31000 \cdot 12}{24 \cdot 0.075 \cdot 0.25 \cdot 1661000} - \frac{22 \cdot 31000 \cdot 12 - 24\cdot 0.075 \cdot 0.25 \cdot 1661000}{27000} - 150 \right) =$$ $$= 300 N$$

Чистая прибыль с одной видеокарты составит \$300.

\subparagraph{Сроки окупаемости при текущем $k = 27000$}

$$ с = \frac{hap}{k} \ln \frac{H_0 + k (t_{\text{be}} - t_0)}{H_0} - 24ew (t_{\text{be}} - t_0) $$ $$ 150 = \frac{22 \cdot 31000 \cdot 12}{27000} \ln \frac{1661000 + 27000 t}{1661000} - 24\cdot 0.075 \cdot 0.25 t, $$ откуда $t$ можно найти численно. А именно, получается $t \approx 46.620 \:\:\text{days}$ --- видеокарта окупится на 47-й день.


\paragraph{\textcolor{RoyalBlue}{Radeon HD 7950}} 

Для этой видеокарты $h = 21$, $w = 0.2$, $c = 170$.

\subparagraph{Случай неизменного хэшрейта}  Подставляя, имеем: $$\text{profit} (t) = Nt \left( \frac{hap}{H + Nh} - 24ew \right) - Nc \approx Nt \left( \frac{hap}{H} - 24ew \right) - Nc = $$ $$= Nt \left( \frac{21 \cdot 31000 \cdot 12}{1661000} - 24 \cdot 0.075 \cdot 0.2 \right) - 170N = 4.343 Nt - 170N $$ Точка выхода на окупаемость $$t = \frac{170}{4.343} \approx 39.143 \:\:\text{days}$$

\subparagraph{Как должен расти хэшрейт, чтобы окупить вложения?}

Неравенство на $k$ $$k < \frac{hap}{c} \ln \frac{hap}{24ew H_0} - \frac{hap - 24ew H_0}{c} =$$ $$= \frac{21 \cdot 31000 \cdot 12}{170} \ln \frac{21 \cdot 31000 \cdot 12}{24\cdot 0.075 \cdot 0.2 \cdot 1661000} -$$ $$- \frac{21 \cdot 31000 \cdot 12 - 24\cdot 0.075 \cdot 0.2 \cdot 1661000}{170} = 75659$$

Таким образом, $k$ должно быть меньше, чем $75659$ (Mhash/s)/day. Это означает, что для окупаемости хэшрейт должен расти меньше, чем на 75 Ghash/s в день.


\subparagraph{Чему будет равна прибыль с одной видеокарты при текущем $k = 27000$?}

$$ \text{net profit} = N \left( \frac{hap}{k} \ln \frac{hap}{24ew H_0} - \frac{hap - 24ew H_0}{k} - c \right) = $$ $$= N \left( \frac{21 \cdot 31000 \cdot 12}{27000} \ln \frac{21 \cdot 31000 \cdot 12}{24 \cdot 0.075 \cdot 0.2 \cdot 1661000} - \frac{21 \cdot 31000 \cdot 12 - 24\cdot 0.075 \cdot 0.2 \cdot 1661000}{27000} - 170 \right) =$$ $$= 306.369 N$$


Чистая прибыль с одной видеокарты составит \$306.


\subparagraph{Сроки окупаемости при текущем $k = 27000$}

$$ с = \frac{hap}{k} \ln \frac{H_0 + k (t_{\text{be}} - t_0)}{H_0} - 24ew (t_{\text{be}} - t_0) $$ $$ 170 = \frac{21 \cdot 31000 \cdot 12}{27000} \ln \frac{1661000 + 27000 t}{1661000} - 24 \cdot 0.075 \cdot 0.2 \cdot t, $$ откуда $t$ можно найти численно. Получается, что $t \approx 57.383 \:\:\text{days}$ --- видеокарта окупится на 58-й день.


\paragraph{\textcolor{RoyalBlue}{Radeon R9 280X}} \subparagraph{Случай неизменного хэшрейта} Для этой видеокарты $h = 25$, $w = 0.25$, $c = 250$. Подставляя, имеем: $$\text{profit} (t) = Nt \left( \frac{hap}{H + Nh} - 24ew \right) - Nc \approx Nt \left( \frac{hap}{H} - 24ew \right) - Nc = $$ $$= Nt \left( \frac{25 \cdot 31000 \cdot 12}{1661000} - 24 \cdot 0.075 \cdot 0.25 \right) - 250N = 5.149 Nt - 250N $$ Точка выхода на окупаемость $$t = \frac{250}{5.149} \approx 48.553 \:\:\text{days}$$

\subparagraph{Как должен расти хэшрейт, чтобы окупить вложения?}

Неравенство на $k$ $$k < \frac{hap}{c} \ln \frac{hap}{24ew H_0} - \frac{hap - 24ew H_0}{c} =$$ $$= \frac{25 \cdot 31000 \cdot 12}{250} \ln \frac{25 \cdot 31000 \cdot 12}{24\cdot 0.075 \cdot 0.25 \cdot 1661000} -$$ $$- \frac{25 \cdot 31000 \cdot 12 - 24\cdot 0.075 \cdot 0.25 \cdot 1661000}{250} = 59575$$

Таким образом, $k$ должно быть меньше, чем $59575$ (Mhash/s)/day. Это означает, что для окупаемости хэшрейт должен расти меньше, чем на 59 Ghash/s в день.


\subparagraph{Чему будет равна прибыль с одной видеокарты при текущем $k = 27000$?}

$$ \text{net profit} = N \left( \frac{hap}{k} \ln \frac{hap}{24ew H_0} - \frac{hap - 24ew H_0}{k} - c \right) = $$ $$= N \left( \frac{25 \cdot 31000 \cdot 12}{27000} \ln \frac{25 \cdot 31000 \cdot 12}{24 \cdot 0.075 \cdot 0.25 \cdot 1661000} - \frac{25 \cdot 31000 \cdot 12 - 24\cdot 0.075 \cdot 0.25 \cdot 1661000}{27000} - 250 \right) =$$ $$= 301.619 N$$


Чистая прибыль с одной видеокарты составит \$301.


\subparagraph{Сроки окупаемости при текущем $k = 27000$}

$$ с = \frac{hap}{k} \ln \frac{H_0 + k (t_{\text{be}} - t_0)}{H_0} - 24ew (t_{\text{be}} - t_0) $$ $$ 250 = \frac{25 \cdot 31000 \cdot 12}{27000} \ln \frac{1661000 + 27000 t}{1661000} - 24 \cdot 0.075 \cdot 0.25 \cdot t, $$ откуда $t$ находится численно. Находим: $t \approx 79.520 \:\:\text{days}$, так что майнинг на такой видеокарте окупится на 80-й день.


## When will Ethereum abandon PoW mining for PoS?

Due to conceptual stage of Casper development, one cannot provide a correct estimate for future PoS mining profit at the moment. Ethereum team reports it will happen <<at some time in 2017>>. Stephan Tual estimates this as 18 months from the network start (i.e. january 2017).



## Can I profit well on mining?


In 2016 mining is hard business with very unclear profit perspectives. Those who decided to enter this business:

1. find a place with industrial electricity that is as cheap as possible (e.g. nearby powerplant) 
2. rent an abandoned warehouse 
3. buy a huge amount of specific (ASICs) or non-specific (GPUs) hardware 
4. configure them and turn on


The perspectives are obscure. By March 2016 Bitcoin total hashing power [fluctuates around](https://blockchain.info/ru/charts/hash-rate) $1.2 \cdot 10^{18}$ hashes per second. On average, 3600 bitcoins are mined every day; if an enterpreneur wants to earn 1 BTC a day by mining, his hashing power $p$ should constitute roughly $1/3600$ of total network hashrate. Let's write it in equation: $$\frac{p}{1.2 \cdot 10^{18} + p} = \frac{1}{3600},$$ where $p$ is hashing power to be acquired (bought or produced).

It's pretty easy to solve this equation. Since $1/3600$ is small fraction, $p \ll 1.2 \cdot 10^{18}$ holds, so $$\frac{p}{1.2 \cdot 10^{18} + p} \approx \frac{p}{1.2 \cdot 10^{18}}.$$ Thus we finally obtain $$p = 1.2 \cdot 10^{18} \cdot \frac{1}{3600} = 3.33 \cdot 10^{14} \frac{\text{hash}}{\text{s}} = 333 \frac{\text{Thash}}{\text{s}}$$

Thus, for our purpose (to earn 1 BTC/day by mining) we should buy sha256-hashing hardware that can calculate 333 Thash/s.

By March 2016 AntMiner S5+ is the rig with highest hashrate. Its hashing power is 7.7 Thash/s and it can be purchased for $2307 (shipping cost excluded). To achieve 333 Thash/s, one should buy 43 of them, with expenses totalling to $100k. Earning 1 BTC per day (w.r.t. March 2016 prices, 1 BTC = $415), we reach breakeven point by day 239. By this day, total network hashrate can grow twice, thrice and to the moon; in reality, our revenue will become lower every day, and our investments will not always break even. In this reasoning, we didn't take into account electricity, staff and warehouse rent expenses.

Moreover, in June 2016 the next halving will happen --- according to Bitcoin protocol, every 210000 blocks block reward [becomes twice lower](https://en.bitcoin.it/wiki/Controlled_supply). In terms of bitcoin, daily mining profit will fall twice. However, this does not mean necessarily losses --- if BTC/USD exchange rate grows more than twice at the time, miners wouldn't earn less. As you see, mining profitability highly depends on bitcoin exchange rate, since miners each in bitcoin and spend (buy rigs, pay for electricity) in fiat currencies.

Mining ecosystem resembles me of California gold rush at the moment --- by that time, those who earned more were device manufacturers. At least there's a well-known fact: when first ASICs started shipping, some buyers posted on Bitcointalk evidences of manufacturing company mining on those devices prior to shipping.



# What else can be done with GPUs?

When old GPUs become unprofitable, one should either sell them to metal buyers, sell them to gamers, or start mining on multipools. Selling to metal buyers is preferrable; one can sell metal buyers for 10% of GPU purchase price.