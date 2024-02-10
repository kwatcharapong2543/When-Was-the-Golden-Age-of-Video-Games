# When-Was-the-Golden-Age-of-Video-Games
Trainning datacamp

{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {
    "dc": {
     "key": "7"
    },
    "deletable": false,
    "editable": false,
    "run_control": {
     "frozen": true
    },
    "tags": [
     "context"
    ]
   },
   "source": [
    "## 1. The ten best-selling video games\n",
    "<p><img src=\"https://assets.datacamp.com/production/project_1413/img/video_game.jpg\" alt=\"A video game player choosing a game to play on Nintendo Switch.\" width=\"400\"></p>\n",
    "<p>Photo by <a href=\"https://unsplash.com/@retromoon\">Dan Schleusser</a> on <a href=\"https://unsplash.com\">Unsplash</a>.</p>\n",
    "<p>Video games are big business: the global gaming market is projected to be worth more than $300 billion by 2027 according to <a href=\"https://www.mordorintelligence.com/industry-reports/global-gaming-market\">Mordor Intelligence</a>. With so much money at stake, the major game publishers are hugely incentivized to create the next big hit. But are games getting better, or has the golden age of video games already passed?</p>\n",
    "<p>In this project, we'll explore the top 400 best-selling video games created between 1977 and 2020. We'll compare a dataset on game sales with critic and user reviews to determine whether or not video games have improved as the gaming market has grown.</p>\n",
    "<p>Our database contains two tables. We've limited each table to 400 rows for this project, but you can find the complete dataset with over 13,000 games on <a href=\"https://www.kaggle.com/holmjason2/videogamedata\">Kaggle</a>. </p>\n",
    "<h3 id=\"game_sales\"><code>game_sales</code></h3>\n",
    "<table>\n",
    "<thead>\n",
    "<tr>\n",
    "<th style=\"text-align:left;\">column</th>\n",
    "<th>type</th>\n",
    "<th>meaning</th>\n",
    "</tr>\n",
    "</thead>\n",
    "<tbody>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>game</code></td>\n",
    "<td>varchar</td>\n",
    "<td>Name of the video game</td>\n",
    "</tr>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>platform</code></td>\n",
    "<td>varchar</td>\n",
    "<td>Gaming platform</td>\n",
    "</tr>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>publisher</code></td>\n",
    "<td>varchar</td>\n",
    "<td>Game publisher</td>\n",
    "</tr>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>developer</code></td>\n",
    "<td>varchar</td>\n",
    "<td>Game developer</td>\n",
    "</tr>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>games_sold</code></td>\n",
    "<td>float</td>\n",
    "<td>Number of copies sold (millions)</td>\n",
    "</tr>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>year</code></td>\n",
    "<td>int</td>\n",
    "<td>Release year</td>\n",
    "</tr>\n",
    "</tbody>\n",
    "</table>\n",
    "<h3 id=\"reviews\"><code>reviews</code></h3>\n",
    "<table>\n",
    "<thead>\n",
    "<tr>\n",
    "<th style=\"text-align:left;\">column</th>\n",
    "<th>type</th>\n",
    "<th>meaning</th>\n",
    "</tr>\n",
    "</thead>\n",
    "<tbody>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>game</code></td>\n",
    "<td>varchar</td>\n",
    "<td>Name of the video game</td>\n",
    "</tr>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>critic_score</code></td>\n",
    "<td>float</td>\n",
    "<td>Critic score according to Metacritic</td>\n",
    "</tr>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>user_score</code></td>\n",
    "<td>float</td>\n",
    "<td>User score according to Metacritic</td>\n",
    "</tr>\n",
    "</tbody>\n",
    "</table>\n",
    "<p>Let's begin by looking at some of the top selling video games of all time!</p>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {
    "dc": {
     "key": "7"
    },
    "tags": [
     "sample_code"
    ]
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "10 rows affected.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <tr>\n",
       "        <th>game</th>\n",
       "        <th>platform</th>\n",
       "        <th>publisher</th>\n",
       "        <th>developer</th>\n",
       "        <th>games_sold</th>\n",
       "        <th>year</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>Wii Sports for Wii</td>\n",
       "        <td>Wii</td>\n",
       "        <td>Nintendo</td>\n",
       "        <td>Nintendo EAD</td>\n",
       "        <td>82.90</td>\n",
       "        <td>2006</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>Super Mario Bros. for NES</td>\n",
       "        <td>NES</td>\n",
       "        <td>Nintendo</td>\n",
       "        <td>Nintendo EAD</td>\n",
       "        <td>40.24</td>\n",
       "        <td>1985</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>Counter-Strike: Global Offensive for PC</td>\n",
       "        <td>PC</td>\n",
       "        <td>Valve</td>\n",
       "        <td>Valve Corporation</td>\n",
       "        <td>40.00</td>\n",
       "        <td>2012</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>Mario Kart Wii for Wii</td>\n",
       "        <td>Wii</td>\n",
       "        <td>Nintendo</td>\n",
       "        <td>Nintendo EAD</td>\n",
       "        <td>37.32</td>\n",
       "        <td>2008</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>PLAYERUNKNOWN&#x27;S BATTLEGROUNDS for PC</td>\n",
       "        <td>PC</td>\n",
       "        <td>PUBG Corporation</td>\n",
       "        <td>PUBG Corporation</td>\n",
       "        <td>36.60</td>\n",
       "        <td>2017</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>Minecraft for PC</td>\n",
       "        <td>PC</td>\n",
       "        <td>Mojang</td>\n",
       "        <td>Mojang AB</td>\n",
       "        <td>33.15</td>\n",
       "        <td>2010</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>Wii Sports Resort for Wii</td>\n",
       "        <td>Wii</td>\n",
       "        <td>Nintendo</td>\n",
       "        <td>Nintendo EAD</td>\n",
       "        <td>33.13</td>\n",
       "        <td>2009</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>Pokemon Red / Green / Blue Version for GB</td>\n",
       "        <td>GB</td>\n",
       "        <td>Nintendo</td>\n",
       "        <td>Game Freak</td>\n",
       "        <td>31.38</td>\n",
       "        <td>1998</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>New Super Mario Bros. for DS</td>\n",
       "        <td>DS</td>\n",
       "        <td>Nintendo</td>\n",
       "        <td>Nintendo EAD</td>\n",
       "        <td>30.80</td>\n",
       "        <td>2006</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>New Super Mario Bros. Wii for Wii</td>\n",
       "        <td>Wii</td>\n",
       "        <td>Nintendo</td>\n",
       "        <td>Nintendo EAD</td>\n",
       "        <td>30.30</td>\n",
       "        <td>2009</td>\n",
       "    </tr>\n",
       "</table>"
      ],
      "text/plain": [
       "[('Wii Sports for Wii', 'Wii', 'Nintendo', 'Nintendo EAD', Decimal('82.90'), 2006),\n",
       " ('Super Mario Bros. for NES', 'NES', 'Nintendo', 'Nintendo EAD', Decimal('40.24'), 1985),\n",
       " ('Counter-Strike: Global Offensive for PC', 'PC', 'Valve', 'Valve Corporation', Decimal('40.00'), 2012),\n",
       " ('Mario Kart Wii for Wii', 'Wii', 'Nintendo', 'Nintendo EAD', Decimal('37.32'), 2008),\n",
       " (\"PLAYERUNKNOWN'S BATTLEGROUNDS for PC\", 'PC', 'PUBG Corporation', 'PUBG Corporation', Decimal('36.60'), 2017),\n",
       " ('Minecraft for PC', 'PC', 'Mojang', 'Mojang AB', Decimal('33.15'), 2010),\n",
       " ('Wii Sports Resort for Wii', 'Wii', 'Nintendo', 'Nintendo EAD', Decimal('33.13'), 2009),\n",
       " ('Pokemon Red / Green / Blue Version for GB', 'GB', 'Nintendo', 'Game Freak', Decimal('31.38'), 1998),\n",
       " ('New Super Mario Bros. for DS', 'DS', 'Nintendo', 'Nintendo EAD', Decimal('30.80'), 2006),\n",
       " ('New Super Mario Bros. Wii for Wii', 'Wii', 'Nintendo', 'Nintendo EAD', Decimal('30.30'), 2009)]"
      ]
     },
     "execution_count": 2,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%%sql\n",
    "postgresql:///games\n",
    "\n",
    "SELECT *\n",
    "FROM game_sales\n",
    "ORDER BY games_sold DESC\n",
    "LIMIT 10;\n",
    "\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "dc": {
     "key": "14"
    },
    "deletable": false,
    "editable": false,
    "run_control": {
     "frozen": true
    },
    "tags": [
     "context"
    ]
   },
   "source": [
    "## 2. Missing review scores\n",
    "<p>Wow, the best-selling video games were released between 1985 to 2017! That's quite a range; we'll have to use data from the <code>reviews</code> table to gain more insight on the best years for video games. </p>\n",
    "<p>First, it's important to explore the limitations of our database. One big shortcoming is that there is not any <code>reviews</code> data for some of the games on the <code>game_sales</code> table. </p>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {
    "dc": {
     "key": "14"
    },
    "tags": [
     "sample_code"
    ]
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * postgresql:///games\n",
      "1 rows affected.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <tr>\n",
       "        <th>count</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>31</td>\n",
       "    </tr>\n",
       "</table>"
      ],
      "text/plain": [
       "[(31,)]"
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%%sql \n",
    "\n",
    "SELECT COUNT(g.game)\n",
    "FROM game_sales g\n",
    "LEFT JOIN reviews r\n",
    "ON g.game = r.game\n",
    "WHERE critic_score IS NULL AND user_score IS NULL;\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "dc": {
     "key": "21"
    },
    "deletable": false,
    "editable": false,
    "run_control": {
     "frozen": true
    },
    "tags": [
     "context"
    ]
   },
   "source": [
    "## 3. Years that video game critics loved\n",
    "<p>It looks like a little less than ten percent of the games on the <code>game_sales</code> table don't have any reviews data. That's a small enough percentage that we can continue our exploration, but the missing reviews data is a good thing to keep in mind as we move on to evaluating results from more sophisticated queries. </p>\n",
    "<p>There are lots of ways to measure the best years for video games! Let's start with what the critics think. </p>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {
    "dc": {
     "key": "21"
    },
    "tags": [
     "sample_code"
    ]
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * postgresql:///games\n",
      "10 rows affected.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <tr>\n",
       "        <th>year</th>\n",
       "        <th>avg_critic_score</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1990</td>\n",
       "        <td>9.80</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1992</td>\n",
       "        <td>9.67</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1998</td>\n",
       "        <td>9.32</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2020</td>\n",
       "        <td>9.20</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1993</td>\n",
       "        <td>9.10</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1995</td>\n",
       "        <td>9.07</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2004</td>\n",
       "        <td>9.03</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1982</td>\n",
       "        <td>9.00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2002</td>\n",
       "        <td>8.99</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1999</td>\n",
       "        <td>8.93</td>\n",
       "    </tr>\n",
       "</table>"
      ],
      "text/plain": [
       "[(1990, Decimal('9.80')),\n",
       " (1992, Decimal('9.67')),\n",
       " (1998, Decimal('9.32')),\n",
       " (2020, Decimal('9.20')),\n",
       " (1993, Decimal('9.10')),\n",
       " (1995, Decimal('9.07')),\n",
       " (2004, Decimal('9.03')),\n",
       " (1982, Decimal('9.00')),\n",
       " (2002, Decimal('8.99')),\n",
       " (1999, Decimal('8.93'))]"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%%sql\n",
    "\n",
    "SELECT g.year, ROUND(AVG(critic_score),2) AS avg_critic_score\n",
    "FROM game_sales g\n",
    "INNER JOIN reviews r\n",
    "ON g.game = r.game\n",
    "GROUP BY year\n",
    "ORDER BY avg_critic_score DESC\n",
    "LIMIT 10;\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "dc": {
     "key": "28"
    },
    "deletable": false,
    "editable": false,
    "run_control": {
     "frozen": true
    },
    "tags": [
     "context"
    ]
   },
   "source": [
    "## 4. Was 1982 really that great?\n",
    "<p>The range of great years according to critic reviews goes from 1982 until 2020: we are no closer to finding the golden age of video games! </p>\n",
    "<p>Hang on, though. Some of those <code>avg_critic_score</code> values look like suspiciously round numbers for averages. The value for 1982 looks especially fishy. Maybe there weren't a lot of video games in our dataset that were released in certain years. </p>\n",
    "<p>Let's update our query and find out whether 1982 really was such a great year for video games.</p>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {
    "dc": {
     "key": "28"
    },
    "tags": [
     "sample_code"
    ]
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * postgresql:///games\n",
      "10 rows affected.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <tr>\n",
       "        <th>year</th>\n",
       "        <th>num_games</th>\n",
       "        <th>avg_critic_score</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1998</td>\n",
       "        <td>10</td>\n",
       "        <td>9.32</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2004</td>\n",
       "        <td>11</td>\n",
       "        <td>9.03</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2002</td>\n",
       "        <td>9</td>\n",
       "        <td>8.99</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1999</td>\n",
       "        <td>11</td>\n",
       "        <td>8.93</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2001</td>\n",
       "        <td>13</td>\n",
       "        <td>8.82</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2011</td>\n",
       "        <td>26</td>\n",
       "        <td>8.76</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2016</td>\n",
       "        <td>13</td>\n",
       "        <td>8.67</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2013</td>\n",
       "        <td>18</td>\n",
       "        <td>8.66</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2008</td>\n",
       "        <td>20</td>\n",
       "        <td>8.63</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2017</td>\n",
       "        <td>13</td>\n",
       "        <td>8.62</td>\n",
       "    </tr>\n",
       "</table>"
      ],
      "text/plain": [
       "[(1998, 10, Decimal('9.32')),\n",
       " (2004, 11, Decimal('9.03')),\n",
       " (2002, 9, Decimal('8.99')),\n",
       " (1999, 11, Decimal('8.93')),\n",
       " (2001, 13, Decimal('8.82')),\n",
       " (2011, 26, Decimal('8.76')),\n",
       " (2016, 13, Decimal('8.67')),\n",
       " (2013, 18, Decimal('8.66')),\n",
       " (2008, 20, Decimal('8.63')),\n",
       " (2017, 13, Decimal('8.62'))]"
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%%sql \n",
    "\n",
    "\n",
    "SELECT g.year,COUNT(g.game) AS num_games,ROUND(AVG(critic_score),2) AS avg_critic_score\n",
    "FROM game_sales g\n",
    "INNER JOIN reviews r\n",
    "ON g.game = r.game\n",
    "GROUP BY year\n",
    "HAVING COUNT(g.game) > 4 \n",
    "ORDER BY avg_critic_score DESC\n",
    "LIMIT 10;\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "dc": {
     "key": "35"
    },
    "deletable": false,
    "editable": false,
    "run_control": {
     "frozen": true
    },
    "tags": [
     "context"
    ]
   },
   "source": [
    "## 5. Years that dropped off the critics' favorites list\n",
    "<p>That looks better! The <code>num_games</code> column convinces us that our new list of the critics' top games reflects years that had quite a few well-reviewed games rather than just one or two hits. But which years dropped off the list due to having four or fewer reviewed games? Let's identify them so that someday we can track down more game reviews for those years and determine whether they might rightfully be considered as excellent years for video game releases!</p>\n",
    "<p>It's time to brush off your set theory skills. To get started, we've created tables with the results of our previous two queries:</p>\n",
    "<h3 id=\"top_critic_years\"><code>top_critic_years</code></h3>\n",
    "<table>\n",
    "<thead>\n",
    "<tr>\n",
    "<th style=\"text-align:left;\">column</th>\n",
    "<th>type</th>\n",
    "<th>meaning</th>\n",
    "</tr>\n",
    "</thead>\n",
    "<tbody>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>year</code></td>\n",
    "<td>int</td>\n",
    "<td>Year of video game release</td>\n",
    "</tr>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>avg_critic_score</code></td>\n",
    "<td>float</td>\n",
    "<td>Average of all critic scores for games released in that year</td>\n",
    "</tr>\n",
    "</tbody>\n",
    "</table>\n",
    "<h3 id=\"top_critic_years_more_than_four_games\"><code>top_critic_years_more_than_four_games</code></h3>\n",
    "<table>\n",
    "<thead>\n",
    "<tr>\n",
    "<th style=\"text-align:left;\">column</th>\n",
    "<th>type</th>\n",
    "<th>meaning</th>\n",
    "</tr>\n",
    "</thead>\n",
    "<tbody>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>year</code></td>\n",
    "<td>int</td>\n",
    "<td>Year of video game release</td>\n",
    "</tr>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>num_games</code></td>\n",
    "<td>int</td>\n",
    "<td>Count of the number of video games released in that year</td>\n",
    "</tr>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>avg_critic_score</code></td>\n",
    "<td>float</td>\n",
    "<td>Average of all critic scores for games released in that year</td>\n",
    "</tr>\n",
    "</tbody>\n",
    "</table>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {
    "dc": {
     "key": "35"
    },
    "tags": [
     "sample_code"
    ]
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * postgresql:///games\n",
      "6 rows affected.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <tr>\n",
       "        <th>year</th>\n",
       "        <th>avg_critic_score</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1990</td>\n",
       "        <td>9.80</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1992</td>\n",
       "        <td>9.67</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2020</td>\n",
       "        <td>9.20</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1993</td>\n",
       "        <td>9.10</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1995</td>\n",
       "        <td>9.07</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1982</td>\n",
       "        <td>9.00</td>\n",
       "    </tr>\n",
       "</table>"
      ],
      "text/plain": [
       "[(1990, Decimal('9.80')),\n",
       " (1992, Decimal('9.67')),\n",
       " (2020, Decimal('9.20')),\n",
       " (1993, Decimal('9.10')),\n",
       " (1995, Decimal('9.07')),\n",
       " (1982, Decimal('9.00'))]"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%%sql \n",
    "\n",
    "SELECT year, avg_critic_score\n",
    "FROM top_critic_years\n",
    "EXCEPT\n",
    "SELECT year, avg_critic_score\n",
    "FROM top_critic_years_more_than_four_games\n",
    "ORDER BY avg_critic_score DESC;\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "dc": {
     "key": "42"
    },
    "deletable": false,
    "editable": false,
    "run_control": {
     "frozen": true
    },
    "tags": [
     "context"
    ]
   },
   "source": [
    "## 6. Years video game players loved\n",
    "<p>Based on our work in the task above, it looks like the early 1990s might merit consideration as the golden age of video games based on <code>critic_score</code> alone, but we'd need to gather more games and reviews data to do further analysis. </p>\n",
    "<p>Let's move on to looking at the opinions of another important group of people: players! To begin, let's create a query very similar to the one we used in Task Four, except this one will look at <code>user_score</code> averages by year rather than <code>critic_score</code> averages.</p>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {
    "dc": {
     "key": "42"
    },
    "tags": [
     "sample_code"
    ]
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * postgresql:///games\n",
      "10 rows affected.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <tr>\n",
       "        <th>year</th>\n",
       "        <th>num_games</th>\n",
       "        <th>avg_user_score</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1997</td>\n",
       "        <td>8</td>\n",
       "        <td>9.50</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1998</td>\n",
       "        <td>10</td>\n",
       "        <td>9.40</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2010</td>\n",
       "        <td>23</td>\n",
       "        <td>9.24</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2009</td>\n",
       "        <td>20</td>\n",
       "        <td>9.18</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2008</td>\n",
       "        <td>20</td>\n",
       "        <td>9.03</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1996</td>\n",
       "        <td>5</td>\n",
       "        <td>9.00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2005</td>\n",
       "        <td>13</td>\n",
       "        <td>8.95</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2006</td>\n",
       "        <td>16</td>\n",
       "        <td>8.95</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2000</td>\n",
       "        <td>8</td>\n",
       "        <td>8.80</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2002</td>\n",
       "        <td>9</td>\n",
       "        <td>8.80</td>\n",
       "    </tr>\n",
       "</table>"
      ],
      "text/plain": [
       "[(1997, 8, Decimal('9.50')),\n",
       " (1998, 10, Decimal('9.40')),\n",
       " (2010, 23, Decimal('9.24')),\n",
       " (2009, 20, Decimal('9.18')),\n",
       " (2008, 20, Decimal('9.03')),\n",
       " (1996, 5, Decimal('9.00')),\n",
       " (2005, 13, Decimal('8.95')),\n",
       " (2006, 16, Decimal('8.95')),\n",
       " (2000, 8, Decimal('8.80')),\n",
       " (2002, 9, Decimal('8.80'))]"
      ]
     },
     "execution_count": 12,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%%sql \n",
    "\n",
    "SELECT g.year, COUNT(g.game) AS num_games, ROUND(AVG(r.user_score),2) AS avg_user_score\n",
    "FROM game_sales g\n",
    "INNER JOIN reviews r\n",
    "ON g.game = r.game\n",
    "GROUP BY YEAR\n",
    "HAVING COUNT(g.game) > 4\n",
    "ORDER BY avg_user_score DESC\n",
    "LIMIT 10;\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "dc": {
     "key": "49"
    },
    "deletable": false,
    "editable": false,
    "run_control": {
     "frozen": true
    },
    "tags": [
     "context"
    ]
   },
   "source": [
    "## 7. Years that both players and critics loved\n",
    "<p>Alright, we've got a list of the top ten years according to both critic reviews and user reviews. Are there any years that showed up on both tables? If so, those years would certainly be excellent ones!</p>\n",
    "<p>Recall that we have access to the <code>top_critic_years_more_than_four_games</code> table, which stores the results of our top critic years query from Task 4:</p>\n",
    "<h3 id=\"top_critic_years_more_than_four_games\"><code>top_critic_years_more_than_four_games</code></h3>\n",
    "<table>\n",
    "<thead>\n",
    "<tr>\n",
    "<th style=\"text-align:left;\">column</th>\n",
    "<th>type</th>\n",
    "<th>meaning</th>\n",
    "</tr>\n",
    "</thead>\n",
    "<tbody>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>year</code></td>\n",
    "<td>int</td>\n",
    "<td>Year of video game release</td>\n",
    "</tr>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>num_games</code></td>\n",
    "<td>int</td>\n",
    "<td>Count of the number of video games released in that year</td>\n",
    "</tr>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>avg_critic_score</code></td>\n",
    "<td>float</td>\n",
    "<td>Average of all critic scores for games released in that year</td>\n",
    "</tr>\n",
    "</tbody>\n",
    "</table>\n",
    "<p>We've also saved the results of our top user years query from the previous task into a table:</p>\n",
    "<h3 id=\"top_user_years_more_than_four_games\"><code>top_user_years_more_than_four_games</code></h3>\n",
    "<table>\n",
    "<thead>\n",
    "<tr>\n",
    "<th style=\"text-align:left;\">column</th>\n",
    "<th>type</th>\n",
    "<th>meaning</th>\n",
    "</tr>\n",
    "</thead>\n",
    "<tbody>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>year</code></td>\n",
    "<td>int</td>\n",
    "<td>Year of video game release</td>\n",
    "</tr>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>num_games</code></td>\n",
    "<td>int</td>\n",
    "<td>Count of the number of video games released in that year</td>\n",
    "</tr>\n",
    "<tr>\n",
    "<td style=\"text-align:left;\"><code>avg_user_score</code></td>\n",
    "<td>float</td>\n",
    "<td>Average of all user scores for games released in that year</td>\n",
    "</tr>\n",
    "</tbody>\n",
    "</table>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {
    "dc": {
     "key": "49"
    },
    "tags": [
     "sample_code"
    ]
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * postgresql:///games\n",
      "3 rows affected.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <tr>\n",
       "        <th>year</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1998</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2008</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2002</td>\n",
       "    </tr>\n",
       "</table>"
      ],
      "text/plain": [
       "[(1998,), (2008,), (2002,)]"
      ]
     },
     "execution_count": 14,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%%sql \n",
    "\n",
    "SELECT year\n",
    "FROM top_critic_years_more_than_four_games\n",
    "INTERSECT\n",
    "SELECT year\n",
    "FROM top_user_years_more_than_four_games;"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "dc": {
     "key": "56"
    },
    "deletable": false,
    "editable": false,
    "run_control": {
     "frozen": true
    },
    "tags": [
     "context"
    ]
   },
   "source": [
    "## 8. Sales in the best video game years\n",
    "<p>Looks like we've got three years that both users and critics agreed were in the top ten! There are many other ways of measuring what the best years for video games are, but let's stick with these years for now. We know that critics and players liked these years, but what about video game makers? Were sales good? Let's find out.</p>\n",
    "<p>This time, we haven't saved the results from the previous task in a table for you. Instead, we'll use the query from the previous task as a subquery in this one! This is a great skill to have, as we don't always have write permissions on the database we are querying.</p>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {
    "dc": {
     "key": "56"
    },
    "tags": [
     "sample_code"
    ]
   },
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      " * postgresql:///games\n",
      "3 rows affected.\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<table>\n",
       "    <tr>\n",
       "        <th>year</th>\n",
       "        <th>total_games_sold</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2008</td>\n",
       "        <td>175.07</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>1998</td>\n",
       "        <td>101.52</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "        <td>2002</td>\n",
       "        <td>58.67</td>\n",
       "    </tr>\n",
       "</table>"
      ],
      "text/plain": [
       "[(2008, Decimal('175.07')),\n",
       " (1998, Decimal('101.52')),\n",
       " (2002, Decimal('58.67'))]"
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "%%sql \n",
    "\n",
    "SELECT g.year, SUM(g.games_sold) AS total_games_sold\n",
    "FROM game_sales g\n",
    "WHERE g.year IN(SELECT year\n",
    "FROM top_critic_years_more_than_four_games\n",
    "INTERSECT\n",
    "SELECT year\n",
    "FROM top_user_years_more_than_four_games)\n",
    "GROUP BY g.year\n",
    "ORDER BY total_games_sold DESC;\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n",
    "\n"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3 (ipykernel)",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.11.5"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}
