# So, who cheated?

## Introduction

In 2021, Major League Baseball had a huge problem on it’s hands; player batting averages were the lowest they had ever [been at .236](https://www.si.com/mlb/2021/06/01/year-of-the-pitcher-again-daily-cover). Pitchers have dominated the sport in the past decade, in part due to advanced analytics, which can give a pitcher the most effective strategy for throwing to a given batter, and will construct a defensive formation that will put fielders into the position where a ball is most likely to be hit. 

This is a problem because the sport is less entertaining when there isn’t any offense. Baseball’s draw as a spectator sport is entirely built on tension, which is created when there are runners on base, particularly when they are in scoring position, and especially when the game is in the late innings and the score is close. When runners are on base, fans of the batting team are watching closely in anticipation of their team scoring, and for fans of the team in the field, they watch nervously hoping their team can get out of it. For both sides, the right amount of offense is what creates the adrenaline response that makes you want to watch the game.

Advanced statistics are here to stay, but MLB had one option to reduce the effectiveness of pitchers; cracking down on foreign substances. Pitchers since the advent of the sport have turned to foreign substances to get a better grip on the baseball; a better grip means higher ball spin rates, which increase the amount of movement on their breaking pitches, and causes their fastball to have less of an arc. Pine tar, sunscreen and rosin, and most recently, [Spider Tack](https://www.nytimes.com/2021/06/08/sports/baseball/gerrit-cole-spider-tack.html), are all used by pitcher to gain an (illegal) advantage over their competitors. 

MLB chose to increase offense by cracking down on foreign substances, and many pitchers were not happy. On June 3rd, they warned players they would be cracking down, and on June 22nd, they instituted random checks for sticky substances throughout the game. Pitchers were mad, arguing that a better grip kept batters safe, and that an abrupt change to the way they had to deliver could leave to injuries (see [Tyler Glasnow](https://www.notion.so/Who-Cheated-a11717ab8c8c4db4ad1432ef250976de)).

However, I am not here to be the arbiter of whether this was the right decision or not (it was). I am here to use some math to determine who was cheating. 

## Methodology

To determine a pitcher’s culpability, we divide spin rate data of their fastballs into two groups; before the crackdown (BC), spanning from the start of the season to the end of May, and after the crackdown (AC), from June 22nd to the end of September. For each pitcher we compare these two groups, looking their means and variances to see if there is a difference before and after the crackdown. The less overlap there is, the more confident we can be that they were cheating. 

In more technical terms, we fit a logistic regression over the data, with our dependent (binary) outcome variable being AC vs. BC, and our independent variable being fast ball spin rate. Fitting a logistic regression on the data lets us determine if there is a statistical significant correlation between AC/BC and fastball spin rates. If there is, we can draw determinations on whether they cheated. 

Take for example Richard Rodriguez, the player who our numbers show had the most clear and prominent change in fastball spin rates before and after the crackdown. 

![richard-rodriguez.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6272c0d9-cdf0-4423-bff8-b7b11f5682c4/richard-rodriguez.png)

Each blue dot on this graph is a fastball thrown by Richard Rodriguez. The x-axis on this graph is the fastball spin rate, and the y-axis is whether or the pitch was thrown before (0) or after (1) the crackdown. Blue dots on the top left are pitches before the crackdown, and pitches on the top right are those after the crackdown, and as you can see, there is very little overlap between the two groups, meaning *something* happened between those two time periods that caused Rodriguez’s spin rates to dramatically decrease. 

Our regression line agrees; the steepness of the sigmoid shows that there is only a small range that our model doesn’t have high confidence in predicting whether or not the pitch was before or after the crackdown. The line represents the probability (from 0 to 1) that a pitch at a given spin rate is before the crackdown. For pitches below 2375 RPMs, the model is almost 100% confident that it is after the crackdown, because before the crackdown, Rodriguez never threw a pitch that spun that little. And for pitches above 2550 RPMs, the model is almost 100% confident that it happened before the crackdown, as he never reached above that threshold afterwards. 

To see a prime example of someone who didn’t cheat, we can look at Jordan Montgomery of the New York Yankees. 

![output.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3fbdfa77-9045-4d3b-bb18-cb7f4686a981/output.png)

We can see the means and variances of his pitches before and after the crackdown are more or less identical. The model finds no statistically significant correlation between AC/BC and his spin rates, with the flat regression line indicating that there is no way to guess whether a pitch was before or after the crackdown by looking only at his spin rates.  

## Results

To get our final list of cheaters, we take a look at all pitchers with above 100 fastballs both before and after the crackdown. We look to see if the model has found a statistically significant, negative correlation between AC/BC and spin rates, and verify that the model has a tight enough pseudo R-squared (we pick an arbitrary value of 0.1).

In total, we find 81 statistically verifiable cheaters. A full list will be included at the bottom of this page, but I will briefly go over some of the high profile names on the list. 

To nobody’s surprise, 5 time all-start Gerrit Cole makes our list. Cole was the poster boy for the scandal, in part due to a video of his [fingers sticking to the brim of his hat](https://www.youtube.com/watch?v=VG_Lz9f-ipE) during a game, and mainly because of an interview he gave after the crackdown was announced where he became [visibly uncomfortable](https://www.si.com/mlb/yankees/news/new-york-yankees-starting-pitcher-gerrit-cole-answers-to-sticky-stuff-speculation). Cole’s fastball spin rate average fell from 2561 RPMs to 2387 RPMs, a 174 RPM difference. 

![gerrit-cole.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/39e9c95f-9d11-48d4-94d7-e7f7a82220a2/gerrit-cole.png)

Madison Bumgarner also makes our list. The 4 time All-Star saw the spin rate on his fastball drop from 2490 RPMs to 2136 RPMs, a staggering 354 RPM difference. 

![madison-bumgarner.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6fe22106-9116-4bd3-88e9-962f6f1e6be7/madison-bumgarner.png)

With 9 All-star game appearances and 3 Cy Young awards, future hall-of-fame pitcher Clayton Kershaw is probably the highest profile name on our list. He saw his average from from 2546 RPMs to 2431 RPMs, a 115 RPM difference.

![clayton-kershaw.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3f833855-5811-476a-bbae-3d32e31d4299/clayton-kershaw.png)

This one hurts me the most to include, but last year’s American League MVP and dual threat pitcher / DH Shohei Ohtani makes our list. Ohtani saw his fastball spin rate drop from an average of 2345 RPMs to 2108 RPMs, a 237 RPM difference.

![shohei-ohtani.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dee2e07d-1db3-4948-8bd1-d92cd5353217/shohei-ohtani.png)

## After Thoughts

This is where my “lawyer” said I had to put in a disclaimer to protect myself against defamation. Our model isn’t definitively calling pitchers cheaters, it only says whether there was a statistically significant decrease in fast ball spin rates before and after the foreign substance crackdown. Cheating is the most likely explanation, but this could also be due to injury, or a change in technique.

This is also a likely undercount; we only considered a pitcher a potential cheater if the model had a p-value of below 0.001, meaning there was a less than 0.1% chance that the correlation between AC/BC and spin rates was due to random chance. Statisticians generally define statistical significance as a p-value below 0.05, and if we did so too, and didn't throw out models with less than convincing pseudo r-squared values, there are over 100 more pitchers we add to our put on our list.

## Full List

![Screen Shot 2022-08-07 at 9.45.00 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b05c5c38-457f-43e1-8cdc-5d5b999fe21e/Screen_Shot_2022-08-07_at_9.45.00_PM.png)
