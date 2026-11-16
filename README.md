<div align="center">
🎮 Steam Games Market Dashboard · 2024 – 2026
What 42,950 new Steam releases reveal about pricing, visibility and what players actually love

</div>
Steam is flooded, and most games are never noticed. Around 1,800 new games launch every month, yet 77% never reach even 10 reviews. Players do reward quality, though: 84% of games that get noticed are rated positive, and a handful of hits (Black Myth: Wukong, Helldivers 2, Palworld) take most of the attention.

<div align="center">
🎮 Games Released	🆓 Free-to-Play	💲 Median Price	👻 Under 10 Reviews	👍 Rated Positive
42,950	15.6%	$4.99	77%	84%
</div>
Top Games & Publishers

🎯 Questions This Dashboard Answers
📈 How many games launch on Steam each month, and how fast is that growing?
💲 How are new games priced, and is free-to-play still popular?
👻 How many games actually get noticed?
⭐ How do players rate new releases?
🏆 Which 2024–2026 games are the biggest hits, and which publishers release the most?

🧹 Data Preparation

Python (scripts/prep_data.py)

Step	Why
🗓️ Kept releases from Jan 2024 to Feb 2026	Recent market only; Feb 2026 is the last complete month in the snapshot
💲 Converted sale prices back to list prices	The raw price is the current price, so a $14.99 game on 65% sale would show as $5.24
⭐ Added Steam-style review ratings	Follows Steam's rules, e.g. Overwhelmingly Positive = 95%+ positive and 500+ reviews
🏷️ Grouped list prices into price ranges	Free · Under $5 · $5–9.99 · $10–19.99 · $20–39.99 · $40+
🐧 Added Mac / Linux support flags	Platform-support analysis
🔗 Built a Steam store link for every game	Makes the explorer table clickable
📊 Built a yearly summary table (2014–2025)	Long-term context

📐 Key DAX Measures
DAX
Games Released     = COUNTROWS ( SteamGames )

Free-to-Play %     = DIVIDE ( CALCULATE ( COUNTROWS ( SteamGames ), SteamGames[Pricing] = "Free-to-Play" ),
                              [Games Released] )

Median Paid Price  = CALCULATE ( MEDIAN ( SteamGames[List Price (USD)] ), SteamGames[Pricing] = "Paid" )

-- How many games are effectively invisible?
Unnoticed Games %  = DIVIDE ( CALCULATE ( COUNTROWS ( SteamGames ), SteamGames[Reviews] < 10 ),
                              [Games Released] )

-- Of the games that DID get noticed, how many are rated positive?
Positively Rated % = DIVIDE ( CALCULATE ( COUNTROWS ( SteamGames ), SteamGames[Tier Order] <= 4 ),
                              CALCULATE ( COUNTROWS ( SteamGames ), SteamGames[Reviews] >= 10 ) )

⚙️ Performance note: a RANKX-based "Top 15" across 43,000 games would compare every game with every other game, about 1.8 billion comparisons each time a filter changes. I used Power BI's built-in Top N visual filters instead, which are instant and still follow every slicer.

📊 Dashboard Walkthrough

🎛️ Filters on both pages (synced): Release Year · Genre · Free / Paid · Price Range · Steam Rating

📈 Page 1 · Market Overview
Visual	What it shows
5 KPI cards	Games released · free-to-play share · median price · games with under 10 reviews · positively rated
Monthly releases	New games per month, Jan 2024 – Feb 2026
Releases per year (area)	Steam's growth from 2014 to 2025
Genre bar	Releases by primary genre
Price-range column	How new games are priced
Rating donut	Steam review ratings, including "Too few reviews"

🏆 Page 2 · Top Games & Publishers
Visual	What it shows
Most-reviewed releases	Top 15 hits (reviews are the best public stand-in for sales)
Most played on snapshot day	Top 10 by peak concurrent players, early March 2026
Busiest publishers	Top 10 publishers by number of releases
Game Explorer	Every game: price, reviews, % positive, rating, playtime and a 🔗 Steam store link

💡 Key Insights
1️⃣ Steam is releasing more games than ever
📈 Yearly releases grew 14× in a decade: 1,518 (2014) → 21,659 (2025)
🚀 2025 was up 20% on 2024
📅 Busiest month: November 2025, with 2,250 releases (about 75 a day)
2️⃣ Most games are never noticed
👻 77% of new games got fewer than 10 reviews
🎯 The top 1% of games hold 86% of all reviews
🆓 Free games are the least likely to be noticed: only 8% reached 10 reviews, compared with 50% of games priced $20–39.99
3️⃣ Cheap is the norm
💲 Median paid price: $4.99
📉 45% of new games cost under $5, and only 1.3% cost $40 or more
🆓 Free-to-play is 15.6% of releases
4️⃣ Players are generous
👍 84% of games with 10+ reviews are rated positive
⭐ 245 games earned Overwhelmingly Positive
5️⃣ The hits of 2024 – 2026

Most-Reviewed Release	Reviews	% Positive
🥇	Black Myth: Wukong	1,150,098	97%
🥈	Helldivers 2	1,017,635	76%
🥉	Palworld	380,709	94%
4	7 Days to Die	370,046	89%
5	Marvel Rivals	287,569	80%

🏅 Best-loved big hits (50K+ reviews): Schedule I (98.4%) · Balatro (98.0%) · MiSide (98.0%) · WEBFISHING (98.0%) · Split Fiction (97.5%)

6️⃣ Indies rule the volume
🎨 79% of games are self-published (developer = publisher)
🎮 Action (16K), Casual (10K) and Adventure (9K) lead releases

⚠️ Limitations
Peak players is a one-day snapshot (early March 2026), not an all-time peak
SteamSpy owner estimates were left out: they're unreliable for several big free-to-play games
2026 covers only January – February
The genre is the game's primary genre only (games often carry several)

📚 What I Learned
🧪 Check what a column really means: "price" was the sale price; converting to list price changed the price distribution
⚙️ Performance matters at scale: RANKX across 43K rows is slow, while Top N visual filters are instant
🔗 Some tables should stay unlinked: keeping the long-term trend separate stops filters from distorting it
📏 Use the platform's own rules: Steam's rating labels make the dashboard instantly familiar to gamers
🎨 Theme to the subject: a dark Steam-style design makes the report feel native to its audience

🙏 Credits
Data: Steam Games Dataset by FronkonGames (Steam API + SteamSpy)
Cleaned copy: Jactyle/VideoGame-Analysis
Steam and the Steam logo are trademarks of Valve Corporation. This is an independent analysis project.
<div align="center">
