---
title: Kaggle Solutions
---
Here are the notes to: [[All Competitions]]
### The Goal:
- To identify ALL the techniques used by the best teams
- Why? Because knowing these tips helps you build intuition on what to do. It makes you better

### Why Study Kaggle Competitions?
- Cause people have to go through the entire ml process
- People need to be considerate of computational resources
- Many people have iterated on the same problem -> better ideas
- It's a competition, so people try a lot harder to figure out what works/doesn't
- They aren't motivated to only show positive results. People will talk about their failures as well
- People will post their code. So if there's something confusing, you can read the implementation to fully understand it
- Kaggle writeups are simpler to read than papers.
- Writeups will self-select important topics for you to learn more about, especially if you see it between competitions

### Why Use This Resource:
- I looked at each competition holistically, scouring discussions as if I were actually competing
- I verify nuances by looking at the specific implementations (on Github/Kaggle notebooks)

### General Kaggle Tips:
- Things that work for some teams (models / features) may not work for every team
	- But some features / techniques always works on a problem
- Pretrained neural net embeddings are OP. Just use them, even with small datasets
- Hyperparam tuning won't save you. `garbage features => bad predictions`
- Winning teams try things that aren't done in the public notebooks.
- Trust your CV, not your ego. Don't get attached to implementations that _should_ work
- The best performers typically work the smartest and put in the most work
	- They've found a magic trick that works well
	- Their iteration times are much shorter than yours
		- They have amazing software tools (weights and biases, optuna)
	- They also have lots of computational resources
- If the competition host has a public notebook / research paper, read it! You'll get ideas and may notice things they didn't see.

### How to review Kaggle problems efficiently
1. Read the intro
2. Sort all of the notebooks by most votes (not hottest). this will usually give you an indication of what to do / what the competition is
3. Fill in the objective / input / output fields in the competition template
	1. Learn what the objective function is! (very important)
		1. What are its weaknesses? Do outliers decrease its score?
4. Write down what you learn in the notebook in the popular notebooks
5. Start reading solution notebooks
	- Make sure you read the comments section, because that is where ppl point out important techniques

### Finding worthwhile competitions to look at
1. look for competitions for problem types you haven't solved before
2. look for competitions with a high leaderboard shake-up
	- Shakeup occurs when most people have a poor [[cross validation]], but some people have amazing CV
	    - you can learn how to create a GOOD CV faster by looking at these competitions
    - You can also learn unconventional opinions that are against majority opinion
	- [Here's a list of competitions with high shakeup](https://www.kaggle.com/code/jtrotman/meta-kaggle-competition-shake-up)

- If you want to search for winning solutions using a specific technique, Google: `kaggle 2nd place solution cyclic learning rate`
	- and iterate your search query from `2nd` to `3rd`, `4th`, etc.

### Navigation Tips
- `cmd + k` to search for anything

#### Obsidian Tips
- cmd + shift + leftarrow to select entire line until the bullet (before deleting)
- here's how to resize images: `![[Pasted image 20240129154843.png|400]]`

#### Cool resources:
- https://farid.one/kaggle-solutions/ (has an exhaustive list of all competitions)
- https://www.kaggle.com/code/sudalairajkumar/winning-solutions-of-kaggle-competitions
	- this is good cause they have tags on the types of competitions
- https://notesonai.com/ a cool resource for general ML
