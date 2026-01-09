---
title: "On the Suns and the 2025-26 NBA season"
draft: false
date: 2025-12-16
summary: "Post NBA"
layout: "simple"
---
{{< katex >}}


## Motivation
We are almost through the first third of the 2025-26 NBA season, and as a Suns fan I want to discuss, trough data, the situation of the team and the league in general. As of 2025-12-16, 26 games in, we are 7th in the West with a record of 14-12. Given that we traded Kevin Durant and waived Bradley Beal, many people are deeming this start quite an impressive effort. Well, first I want to recall that last year's Suns were the worst form of this team in the last 6 years, and yet we also started 14-12 through the first 26 games. This fact, combined with the amazing discovery of "nba_api" (https://github.com/swar/nba_api), led me to wonder what the data would actually say about this new team.

## Comparison
The team has changed, that I can't deny. New coach, another great draft with Maluach, Fleming and Koby Brea, and the addition of key pieces in Dillon Brooks and Jalen Green. Before diving into the data, I want to note my reluctance to Jalen Green. I do not believe in his skillset and approach to the game, another high usage low accuracy guard near Booker is a recipe for dissaster. However, due to Jalen's injury we have not seen them play together, thus I will not make any definitive assertions.

Let's look at a comparison of last year's and this year's basic stats and discuss them. Note all stats shown were taken per 100 possessions.
<div style="display:flex; justify-content:center; gap:1rem; flex-wrap:wrap;">

  {{< figure src="/images/NBA_POST/BASE_COMP.png">}}
</div>

The first two rows are what I would call the *Dillon Brooks effect*. We are drawing more personal faults (PFD) and committing more fouls (PF). One should not look at this increase with bad eyes; it is actually a positive thing if handled correctly. Unfortunately Booker did not get the memmo. I take this space to note the amazing jump offensively that Dillon Brooks is having. Right now he has gone from 14 PPG to 21.6 PPG, if he keeps those numbers I would seriously consider him a contender for the MIP, even though he is already a stablished named in the league.

Continuing down the chart, we are recieving more blocks and blocking fewer shots. This is just due to the clear difference in play style between Nurkic (previous center) and Mark Williams (actual center). We are also generating more steals while committing more turnovers. I want to focus on the steals because turnovers are what are driving me insane this season, and we will discuss them later on. We are playing a much more active basketball, mainly thanks to Dillon Brooks. This shift in energy had made almost every player step up in terms of steals, remarking Grayson Allen who is stealing 1 more whole ball.

We are dealing less assists because we don't have KD to draw defensive attention, and now Booker is consistently facing the best defenders. Then the change in rebound distribution is, again, due to the change of center; Nurkic almost only took defensive boards, and Mark Williams is more of an offensive center.
The rest is not that relevant. Percentages changes although impercetible due to scale, are minimal.

Now we diving deeper into second opportunities and how we are dealing with those turnovers.
<div style="display:flex; justify-content:center; gap:1rem; flex-wrap:wrap;">

  {{< figure src="/images/NBA_POST/MISC_COMP.png">}}
</div>

As I mentioned before, turnovers are a problem. As we loose more balls, we are getting penalized. However, this graphic also contains good news. Note that this new rapid style of play is allowing us to convert more off those turnovers. Not only that, the increase in offensive rebounds gives us more points on second chances.
A suns fan might be hopeful reading this and thinking we might do something this year. Well, I feel like it is my job to crush those expectations. Let's now compare ourselves with the rest of the league.

<div style="display:flex; justify-content:center; gap:1rem; flex-wrap:wrap;">

  {{< figure src="/images/NBA_POST/TODAYS_NET_PACE.png">}}
</div>

The graph y-axis is the pace, which represents how fast the team is playing in terms of possessions. It looks something like

\[
   \text{PACE}=\frac{240(\text{Poss} _1+\text{Poss} _2)}{2\times \text{TotalTeamMins}}\]

The x-axis is the net rating, which is simply the difference between offensive rating and defensive rating those, being statistics on how well the team attack and defend. the easy versions used by the nba (https://www.nba.com/stats/help/glossary) are
\[\text{OFFRTG}=100 \times \frac{\text{Points}}{\text{Poss}}\qquad \text{DEFRTG}=100 \times \frac{\text{OppPoints}}{\text{OppPoss}}\]  

Looking at the figure we can see that we are neither playing particularly fast nor winning by a margin. Nevertheless, one could argue that we are not in terrible shape if we look in our near radius. Current seeds 6 (Minessota), 4 (Spurs) and 3 (Lakers) are relatively close in terms of this statistics.

No comment on OKC. FUCK THEM.


It is only natural to see how this map looked last year.
<div style="display:flex; justify-content:center; gap:1rem; flex-wrap:wrap;">

  {{< figure src="/images/NBA_POST/LAST_YEAR_NET_PACE.png">}}
</div>

We can appreciate the change in our pace, but so does almost all the leage in a sense. However, if we check our pace through the first 25 games of the last season, it is almost the same as portrayed in the graph above. It is true that we had better net rating due to that impressive start.
Before moving on, Celtics pace is notably low in both graphs, they play a really three-focused brand of basketball which does not translate into fastbreaks and quick possesions.


## Booker shots distribution

When seeing the Suns these past years I have always felt that Booker was not playing his style of basketball. He went from a 4 APG player to a 7APG player, people like that he is involving his teammates more, but we must take into account the amount of effort that goes to looking for those assists. However, let's see the data.
 
<div style="display:flex; justify-content:center; gap:1rem; flex-wrap:wrap;">

  {{< figure src="/images/NBA_POST/DEMON_CHART.png">}}
</div>
This chart is composed by two. The top one portrays the FGA attempts distribution on the court throughout Booker's career. I left corner threes out because it is not his main shot, and has not changed in volume. The bottom chart represents the FG pertentage of each location on top of eachother. The data is with me in terms that the volume of above the break 3's is getting out of hand, with last year being the highest. Last year split is just ludicrous, not only he shot 470 above the break 3's with a 30% accuracy, he got to the paint more times than mid range shots for the first time in his whole career while having less accuracy on those shots. It is completely baffling to me how no one is paying attention to this, because, it is where all the offense starts. For now, I will not comment on the data of this year's season, the clear less amount of attempts is due to the fact that wea are only a third into the season, and the whopping 29% on threes won't be commented on either for my sanity.

My favourite versions of the Suns where 2020-2021 (the finals team), and 2022-23 when we got KD mid season and were really good in the playoffs, ultimately we lost to Denver who continued to win it all. Now let's look at the chart for those two seasons, what does it have in common?

THE DISTRIBUTION WAS MUCH MORE CONCENTRATED!! Booker was much more versatile those seasons. When you threat with several shots or possibilities the rival deffense must adapt, which is not that easy. Data back what my eyes are seeing, running point is limiting his offense in the sense that the shots he recieves now are much more concentrated in terms of kind.

## Conlcusion

We'll see how the season develop. GO SUNS!

