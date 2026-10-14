# CU-Hockey
Business Analytics

Learn **pandas DataFrames** with real stats for three CU Boulder club hockey teams.

## What's here

| File | What it is |
|---|---|
| [`CU_Hockey_pandas_WarmUp.pdf`](CU_Hockey_pandas_WarmUp.pdf) | Warm-up slides: 10 questions to answer with pandas, plus a bonus challenge |
| [`Week7_Pandas_CU_Hockey_InClass.ipynb`](Week7_Pandas_CU_Hockey_InClass.ipynb) | In-class notebook: walk-through with ✏️ *Your turn* exercises |
| [`cu_hockey_data/`](cu_hockey_data/) | The data. See its [README](cu_hockey_data/README.md) for every column |

The teams: CU Men's D1 (2024-25), CU Men's D2 (2023-24 and 2026-27, in progress) and CU Women's D1 (2024-25). Data comes from the [ACHA](https://www.achahockey.org) and [Big Mountain Hockey Conference](https://www.bigmountainhockey.com) stats pages, pulled 10/14/2026.

## Get started

```bash
git clone https://github.com/iportilla/CU-Hockey.git
cd CU-Hockey
pip install -r requirements.txt
jupyter notebook Week7_Pandas_CU_Hockey_InClass.ipynb
```

Run the notebook from the repo folder, because it loads the data with relative paths like `cu_hockey_data/cu_games.csv`.

## Warm-up questions

1. How many games are in the file, and how many have been played?
2. What's the most penalty minutes one player racked up in a season?
3. Which players scored 20 or more points in a season?
4. Who are CU's top 5 scorers across all three teams?
5. What was CU's biggest win?
6. Which team-season has the best winning percentage?
7. Do CU teams win more often at home than on the road?
8. Which columns have missing values, and why are they missing?
9. Are defensemen taller than forwards?
10. Do left-handed or right-handed shooters score more goals?

**Bonus:** build the standings table. Who finishes first?
