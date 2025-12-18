---
title: "Miscellaneous"
description: "Figures, scripts and random experiments."
---

Here I pretend to dump figures I found interesting or simple experiments that do not require theoretical explanation.

Random walk through Wikipedia: [link](/images/random_walk.html).

The Mathematics network (It takes some time to load): [link](/images/snapshot_2.html).

Top 30 players in FGA with their TS on the first 25 games of the 2025-26 NBA season:

<button type="button"
        onclick="
          const img = document.getElementById('nba-plot');
          if (img.style.display === 'none' || img.style.display === '') {
            img.style.display = 'block';
            this.textContent = 'Hide chart';
          } else {
            img.style.display = 'none';
            this.textContent = 'Show chart';
          }">
  Show chart
</button>

<div id="nba-plot" style="display:none; margin-top:1rem;">
  <img src="/images/NBA_POST/FGA_TS_2025-26.png"
       alt="Top 30 FGA vs TS, first 25 games 2025-26"
       style="max-width:100%; height:auto;">
</div>



