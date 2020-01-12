---
layout: post
title: Can Natural Language Processing help us make sense of the debates?
---

In the past year there has been **6** democratic debates with a total of **22** candidates who have spoken **181864** words for a total of **14 hours, 47 minutes and 24 seconds.**

With so much content, I find it's often difficult to make sense of what's happened.

This blog post aims to tell the story of the democratic debates through data.

Along the way I hope to demonstrate some techniques in machine learning, natural language processing, and data science. Techniques that we can use to make sense of this data.

_Note: The dataset is downloaded from [Rev](https://rev.com) which is a transcription service that provides full transcripts of the debates for free._

# Lets talk about talking
First, let's take a look at how long each candidate spoke over the past 6 debates:

Candidate            | Total Time | Utterances | Average Time
-------------------- | ---------  | ---------- | -----------
Elizabeth Warren	|	1:40:27	|	255	|	0:23
Joe Biden	|	1:33:09	|	278	|	0:20
Bernie Sanders	|	1:27:57	|	219	|	0:24
Pete Buttigieg	|	1:18:08	|	209	|	0:22
Amy Klobuchar	|	1:14:33	|	170	|	0:26
Kamala Harris	|	1:06:39	|	196	|	0:20
Cory Booker	|	1:02:07	|	151	|	0:24
Andrew Yang	|	0:44:15	|	92	|	0:28
Beto O’Rourke	|	0:43:55	|	113	|	0:23
Julian Castro	|	0:37:41	|	94	|	0:24
Tulsi Gabbard	|	0:35:04	|	73	|	0:28
Tom Steyer	|	0:27:18	|	61	|	0:26
Kirsten Gillibrand	|	0:17:43	|	67	|	0:15
Tim Ryan	|	0:16:56	|	48	|	0:21
Michael Bennet	|	0:16:54	|	64	|	0:15
Bill de Blasio	|	0:15:16	|	58	|	0:15
John Delaney	|	0:15:06	|	60	|	0:15
John Hickenlooper	|	0:13:53	|	46	|	0:18
Marianne Williamson	|	0:13:47	|	52	|	0:15
Jay Inslee	|	0:11:57	|	25	|	0:28
Steve Bullock	|	0:10:10	|	32	|	0:19
Eric Swalwell	|	0:04:29	|	21	|	0:12

On average, each time a candidate spoke, they were only able to speak for _**22 seconds**_. The median is _**21 seconds**_. This certainly doesn't not seem like enough time to explain complex policy proposals.

What’s more telling though, is the **relative amount of time** each candidate spoke.

![image]({{ site.baseurl }}/images/speaking-time-all.png)

This chart visually shows the amount of time each candidate spoke relative to the total amount of time all candidates spoke. **The top 6 candidates spoke more than the other 16 candidates combined.**

Obviously part of this comes from the fact that many of the candidates only appeared in one or two debates. Looking at the first debate, the time is much more balanced:

![image]({{ site.baseurl }}/images/speaking-time-first.png)

## Do networks have a bias for popular candidates?
_Note: The polling data is downloaded from Real Clear Politics_

We intuitively understand that candidates who poll higher are given more speaking time. But how true is this? For every candidate, I plotted their poll number against how much time they spoke for each debate.

![image]({{ site.baseurl }}/images/polling-vs-speaking-time-all.png)

In general, this trend holds true with an r-squared score of 0.369. There are however, some notable standouts. The top left corner are candidates who don’t poll well, yet had a lot of speaking time. Senator Klobuchar polled at around 2% during Sixth debate, yet spoke almost twice as much as Joe Biden, who was polling at 32%.

_An r-squared score can tell you how correlated your data is. A score of 1 means perfect correlation, and a score of 0 means no correlation._

## The Andrew Yang conspiracy

There was some [internet buzz](https://www.reddit.com/r/YangForPresidentHQ/comments/e0m8e3/andrew_is_pissed_msnbc_we_are_trending_now/) that MSNBC was [biased against Andrew Yang](https://twitter.com/AndrewYang/status/1198258580996214784) during the fifth debate. Here's what that plot looks like for just the fifth debate:

![image]({{ site.baseurl }}/images/polling-vs-speaking-time-fifth.png)

Andrew Yang polled better than Booker, Klobuchar, Gabbard, and Steyer, and yet only spoke about 6 minutes out of a 2 hour debate.

## Which network followed this rule most closely?

The second debate, hosted by CNN had the strongest correlation (r-squared of 0.848) between polling performance and speaking time, while the sixth debate hosted by PBS had the weakest correlation (r-squared 0.004). However, a common theme in both of them? **Andrew Yang spoke the least**.

![image]({{ site.baseurl }}/images/polling-vs-speaking-time-second.png)

![image]({{ site.baseurl }}/images/polling-vs-speaking-time-sixth.png)

In general though, it seems if you can make it onto the stage, you’ll get at least 7 - 10 minutes of speaking time, regardless of how well you poll. Except for Andrew Yang, who spoke for a measly 3 minutes during the first debate. If I had to stand through a 3 hour debate to talk for just 3 minutes, I'd be pissed too.

Takeaway? **Let Andrew Yang speak more!**

![image]({{ site.baseurl }}/images/andrew-yang-frustrated.jpg)

# On the issues facing America

I trained a text classification model to predict whether a blurb of text is about one of:
* HEALTHCARE
* FOREIGN_POLICY
* GUN_CONTROL
* CIVIL_RIGHTS
* IMMIGRATION
* ECONOMY
* ENVIRONMENT
* GOVERNMENT_REFORM
* EDUCATION
* REPUBLICANS
* OTHER

_Big thanks to the [Snorkel](https://hazyresearch.github.io/snorkel/) team for building the tools to make this possible._

For instance, given a sentence like:

_“My response is Obamacare is working. The way to build this and get to it immediately is to build on Obamacare”_

The model predicts **HEALTHCARE** with 94% confidence.

We can use this model to get an idea of how much time each candidate spends talking about the different issues listed above.

Here is how the democratic candidates allocated their speaking time in aggregate:

![image]({{ site.baseurl }}/images/all-time-spent.png)

With most of the time being allocated to foreign policy, the economy, and healthcare.

Most of this data confirms trends most people already understand. Bernie Sanders spends more time talking about healthcare than Joe Biden.

![image]({{ site.baseurl }}/images/biden-time-spent.png)

![image]({{ site.baseurl }}/images/sanders-time-spent.png)

Elizabeth Warren seems to have the most balanced time allocation of all the candidates, spending more time than others talking about government reform and education.

![image]({{ site.baseurl }}/images/warren-time-spent.png)

I won’t bore you with 22 different breakdowns since many of them look very similar. However there are some notable exceptions.

### Single issue candidates (looking at you Senator Gabbard)

A few candidates spend a disproportionate	amount of time (relative to other candidates) on specific issues.

Andrew Yang’s platform is based on establishing a universal basic income, which is reflected in his coverage of the economy.

![image]({{ site.baseurl }}/images/yang-single-issue.png)

Tom Steyer is a businessman who became a climate activist, so he tends to speak more about the economy and the environment.

![image]({{ site.baseurl }}/images/steyer-single-issue.png)

But everyone pales in comparison to Tulsi Gabbard, who spent almost two thirds of her time talking about foreign policy. Understandable, given her background as a veteran who served in Iraq and Kuwait, and a fierce opposition of American interventionism.

![image]({{ site.baseurl }}/images/gabbard-single-issue.png)

# Dammit Joe, can you just let me finish?

When I was in elementary, I joined our schools debate club. Actually my parents made me join because they thought it would help with public speaking (it didn't). The topics were less consequential, like whether zoos should exist or whether chores had a positive influence. (We also were given more than 23 seconds to make a case). I don't remember much because, like other kids in that club, I never attended. But, I vaguely remember a rule against one debater interrupting another.

It certainly seems on the big stage, there are many instances of one candidate interrupting another. How often does this happen and are some candidates more eager to interrupt than others? I defined an "interruption" as a **candidate speaking without being asked a question by a moderator**.

Of the 14 hours and 47 minutes the candidates spoke, **55 minutes, 31 seconds of that was one candidate interrupting another**.

Here are the worst offenders:

![image]({{ site.baseurl }}/images/interruption-number.png)

Joe Biden has interrupted his peers 54 times over the past 6 debates, out of the 278 he said something. In other words, **19% of the time Joe Biden said something, he was cutting off someone else**.

![image]({{ site.baseurl }}/images/biden-yelling.jpg)

In his defense, I took a look at what he said during these interruptions, and many were responding to criticisms by other candidates.

While Joe Biden has a **high number of interruptions**, other candidates have a **high percentage of time spent interrupting**. John Delaney only spoke for 15 minutes and 6 seconds in total, but, 1 minute 57 seconds of that time was via an interruption, which is about 13%.

![image]({{ site.baseurl }}/images/interruption-percentage.png)

# The elephant in the room
![image]({{ site.baseurl }}/images/trump-smug.jpg)

Throughout the election democrats have continuously stressed the importance of focusing on real issues rather than just being ["anti-Trump"](https://www.nbcnews.com/politics/politics-news/schumer-warns-democrats-can-t-just-be-anti-trump-n847186). Did the current crop of democrats follow their own advice? Tdlr; kinda?

![image]({{ site.baseurl }}/images/utterances-trump.png)

Steve Bullock was only given 25 opportunities to speak, and in 7 of those, he mentioned Trump. Curiously at the top is Andrew Yang, who has stressed the importance of not obsessing over Trump so often that he mentions him at a higher rate than basically every other Democrat. He mentions Trump in 14 out of 92 utterances (he actually References Trump directly 28 times). Kamala Harris, Cory Booker and Amy Klobuchar are tied for first, mentioning Trump in 17 of their utterances. In total, Donald Trump was referenced 330 times across all the candidates.

However, the "top" candidates (who I'm considering to be Biden, Warren, Sanders, and Buttigieg) were less interested in talking about Trump. They only mentioned Trump in about 5% of their statements, combining for 52 mentions out of the 961 times they spoke.

## [Come back, Barack](https://www.youtube.com/watch?v=ZkPSbp3zTfo)

Of people who were mentioned that were not on stage, Barack Obama leads with 59, Mitch McConnell 23 and Vladimir Putin 18.

Interestingly, we can also paint a picture of current American foreign policy, by looking at foreign countries that were mentioned.

![image]({{ site.baseurl }}/images/mentioned-countries.png)

China is mentioned 87 times, followed by Afghanistan (52), Russia (34), Iraq (32) and Iran (30). Undoubtedly, mentions of Iran will surge after [what](https://www.cbsnews.com/news/qassem-soleimani-iran-expert-calls-strike-that-killed-iranian-general-stunningly-stupid-and-counterproductive-2020/) [has](https://www.washingtonpost.com/national-security/2020/01/11/irans-attack-us-forces-exposes-pentagons-challenge-with-stopping-ballistic-missiles/) [happened](https://www.washingtonpost.com/world/europe/ukraine-requests-intelligence-on-crashed-airliner-as-iran-denies-missile-attack/2020/01/10/38e21ad8-332d-11ea-a053-dc6d944ba776_story.html).

## Do more popular candidates get more heat?

It is often said that as candidates become more popular in the polls, other candidates will "attack" or reference them more often in debates. [Pete Buttigieg's latest debate](https://www.youtube.com/watch?v=CMgQu1GjSmk) comes to mind. What happens if we plot each candidates poll numbers against how many time they were mentioned in each debate? (Doesn't include moderator mentions).

![image]({{ site.baseurl }}/images/poll-number-vs-references.png)

In general, there is some correlation that exists, but it isn't strong (r-squared = 0.35).

The top right of the graph shows candidates who poll well who are mentioned by their peers often. The data suggests that if you are mentioned a lot, you are probably polling well. However, some candidates to manage to fly under the radar. Joe Biden and John Delaney were mentioned about the same amount during the fourth and fifth debates. Biden polls around 30% while Delaney polls at around 0%.

# Obligatory word clouds

Every other post about NLP seems to have one of these sections. To this day I'm not sure what word clouds could actually be used for, but they certainly look cool. Here are a few I found interesting.

#### Bernie Sanders

_healthcare, profit, system_

![image]({{ site.baseurl }}/images/sanders-word-cloud.png)


#### Andrew Yang

_job, technology, money, economy_

![image]({{ site.baseurl }}/images/yang-word-cloud.png)

#### Elizabeth Warren

_problem, student loan, families, law_

![image]({{ site.baseurl }}/images/warren-word-cloud.png)

#### Amy Klobuchar

_bill, state, experience_

![image]({{ site.baseurl }}/images/klobuchar-word-cloud.png)

Here's Joe Biden's in the shape of a kangaroo.

![image]({{ site.baseurl }}/images/biden-word-cloud.png)

These animals are having a hard time in Australia right now. If you enjoyed this post, please consider paying it forward to an organization helping with the crisis. Here are a couple to get you started:
* **[WIRES](https://www.wires.org.au/blog/emergency-donations-to-help-wildlife)** _The Wildlife Information, Rescue and Education Service is accepting donations to fund the rescue and care of animals affected by the fires. In December, WIRES received more than 20,000 calls and volunteers attended more than 3,300 rescues._
* **[Australian Red Cross](https://www.redcross.org.au/campaigns/disaster-relief-and-recovery-donate)** _The Australian Red Cross has assisted more than 18,600 people affected by the fires. They are accepting donations for bushfire relief efforts._
* **[Koala Hospital Port Macquarie](https://www.koalahospital.org.au/shop/donation)** _This koala hospital in New South Wales is accepting donations to fund the rescue, treatment and release of koalas._
* **[World Wildlife Fund Australia](https://donate.wwf.org.au/donate/koala-crisis/koala-crisis)** _This chapter of the international wildlife conservation organization is accepting donations to care for injured wildlife and, when the fires clear, to plant 10,000 native trees in critical koala habitat._

![Koala Rescue]({{ site.baseurl }}/images/koala-rescue.jpeg)

Find the code for the project [here](https://github.com/czhu12/czhu12.github.io). Images are [here](https://github.com/czhu12/czhu12.github.io/tree/master/images)
