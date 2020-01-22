---
layout: post
title: What are we normalizing for?
---

Statistics is the science of answering questions through the data.

The gender pay gap debate falls victim to this. Part of the reason why this debate is still on-going, despite the abundance of data that exists, is that statisticians can't seem to agree how to interpret at the data.

Before going further, I'd like to say that I'm not taking a position on the gender wage gap. I just want to highlight the deficiencies in these debates and to offer an alternative way to think about these debates, as well as a framework for thinking about statistical claims in general. Namely, **these debates make no sense without first agreeing on an underlying model of how the data is generated**.

The question most sociologists are debating is this:

_"Is gender predictive of discrimination which is predictive of a wage gap?"_

Here's an alternative view of this question:

![image]({{ site.baseurl }}/images/normalization/wage-gap-question.png)

Because "discrimination" isn't really measurable in the traditional sense, it's unobservable. Instead, we measure the correlation between the two observable variables in this diagram. Gender and wage.

### Wait... Correlation is not Causation?

It's a well established fact that women on average make 82% of men. But, if you recall from high school statistics: "correlation does not imply causation".

When Jordan Peterson was confronted with this fact, he argued _"If you're a social scientist worth your salt, you never do a univariate analysis"_. What he means is that we need to normalize for certain factors. One factor he mentions is occupation. Let's think about that a bit deeper.

What Peterson arguing is that perhaps, one of the reason for men making more than women is actually due to differences in occupations. Maybe through a mechanism like this:

![image]({{ site.baseurl }}/images/normalization/no-discrimination.png)

### Sidebar on Statistical Confounders

In this case, age is a **confounder**. It creates a correlation between two variables where no causation exists. These are found everywhere in statistics. For instance, there is a correlation between the amount of milk consumption per capita, and the number of Nobel prizes a country wins.

![image]({{ site.baseurl }}/images/normalization/chocolate-vs-nobel-prizes.jpg)

Despite this information, I doubt you'd be willing to believe that milk consumption causes Nobel prizes, because "correlation does not imply causation"

Astoundingly, [some people](https://healthland.time.com/2012/10/12/can-eating-chocolate-help-you-win-a-nobel-prize/) still overlook this rule.

> For the U.S. (to win one additional Nobel prize), we should consume an extra 125 million kg (275.6 million lbs.) of chocolate a year.

Indeed, this correlation is likely due to a confounder: wealth. We can see this is we plot wealth vs Nobel prizes. (Countries that have more to spend on chocolate probably also have more to spend on education).

![image]({{ site.baseurl }}/images/normalization/wealth-vs-nobel-prizes.jpg)

If we normalize against wealth, we would see that the correlation between Nobel prizes / wealth and chocolate is weaker.

Jordan Peterson is essentially arguing that age may well have an effect on the gender vs wage correlation the same way wealth affects the Nobel prize vs chocolate correlation.

We can apply the same remedy: normalize against occupation, which case, the correlation is demonstrated to be weaker.

### Damn these Confounding Confounders

In this case, we implicitly creating a model of the world:

![image]({{ site.baseurl }}/images/normalization/dag-wealth-nobel-prizes.png)

However, we are back to the same problem. Is there another confounder of this correlation? I can again introduce another confounder.

Since our understanding of genetics is limited, this confounder may well be unprovable.

Therein lies the fundamental weakness in statistics. **Statistics can only demonstrate correlation, never prove causation**.

### What are we normalizing for?

I hope I've convinced you that while data is objective, the interpretation (and therefore, utility) of data is highly subjective. Statisticians try to get around this by normalizing for every potential confounder, as a means of uncovering the true relationship between gender and wage. Age, personality, occupation, college education, marital status, etc. But, this can also cause problems. Let's create a model of the data generation process to see why.

In this model, it makes sense to normalize against occupation, since it's a confounder. The story this model tells is that women tend to choose different (lower paying) occupations than men do, and therefore, this explain's some of the wage difference. Indeed, this is an argument that is made by people who claim the wage gap isn't as big as first glance.

However, here is an alternative model of the data generation process:

This model tells a completely different story. In this model, women choose different occupations due to discriminatory pressures.

In this case, **normalizing occupation removes the very mechanism through which women are underpaid due to discrimination**. To put it another way, if we only look at women in high paying occupations, they would make the same as men. But women are denied access to these higher paying jobs due to discrimination. Normalizing for occupation hides this.

The issue is that model 1 and model 2 can produce the exact same data, due to the fact that the "discrimination" variable is not measurable. Even if it is measurable, someone else can come along and suggest another unmeasurable confounder of discrimination vs wage.

https://www.heritage.org/jobs-and-labor/commentary/pay-gap-myth-ignores-womens-intentional-job-choices
https://www.theatlantic.com/business/archive/2016/07/paygap-discrimination/492965/
https://www.salon.com/2019/02/19/why-women-are-dropping-out-of-stem-careers/
https://hbr.org/2016/08/why-do-so-many-women-who-study-engineering-leave-the-field

https://healthland.time.com/2012/10/12/can-eating-chocolate-help-you-win-a-nobel-prize/

Thanks to the fantastic work of Judea Pearl. If this was interesting, check out his [book](https://www.amazon.com/Book-Why-Science-Cause-Effect/dp/046509760X).
