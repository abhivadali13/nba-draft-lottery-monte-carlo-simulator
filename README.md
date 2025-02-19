# NBA Draft Lottery: A Monte Carlo Simulation

## Instructions:

In order to use this simulator:

 - clone this repository into your local machine
 - open up the .ipynb files in Jupyter Notebook or upload the files to Google Drive and open the .ipynb files in Google Colab
 - make sure all the files are in the same directory, and run

## Project Files:

- 'nbadraftlottery_functions.py': contains all the functions for the simulator + docstrings + doctests
- 'nbadraftlottery-simulator.ipynb': only contains the user input section of the simulator, uses 'nbadraftlottery_functions.py' to abstract away functions and provide ease-of-use for the user
- 'vadali_abhi_nbadraftlottery_montecarlosimulation.ipynb' contains all the functions + docstrings + main section + walkthrough of code with markdown as well...the most comprehensive file for first-time users to truly understand the code

## Project Background:

The NBA Draft Lottery determines the order that the 14 worst teams will select upcoming talent in the NBA Draft. 

- Every team is assigned a certain set of odds to pick #1 overall in the draft, with worse-performing teams having the higher chances. 
- The worst three teams will have equal odds at selecting #1.

A typical lottery ball machine is used to carry out the NBA Draft Lottery. 

![image](https://user-images.githubusercontent.com/46533891/116900598-87018a00-abfe-11eb-9491-bbfd60310a51.png)

- Fourteen Ping Pong Balls (Numbered 1 to 14) are placed in a lottery machine.
- Each 4 digit combination of the 14 balls is assigned to a certain team. There are a total of 1,001 possible combinations, of which 1 is discarded. 
  - The teams with the lowest records are assigned the most number of combinations based on their odds. 
- Drawings are conducted to select the first four picks. The remaining picks are determined in inverse order of the teams’ records. 

In the Drawing Process, for each combination drawn, the lottery machine is mixed for 20 seconds before drawing the first ball and 10 seconds before every subsequent ball. 

- The team that has been assigned the combination that is drawn will receive the pick (1-4) in question.
- If the same team was drawn twice, the result is discarded. If the unassigned sequence is drawn, the result is also discarded.

![Screen Shot 2021-05-03 at 11 00 42 AM](https://user-images.githubusercontent.com/46533891/116900841-d47df700-abfe-11eb-8d4e-8b8e6a98cb38.png)

For more information on this process, feel free to visit: https://www.nba.com/nba-draft-lottery-explainer.

## Project Purpose:

In this project, I carry out the following steps:

- Replicate, and perform a Monte Carlo simulation of, the NBA Draft Lottery and calculate aggregate statistics of which teams are given which picks
  - Do this using the ping-pong ball method outlined above and using a multinomial distribution.

- Apply my own modifications to the NBA Draft Lottery.
  - Run a simulation of the NBA Draft Lottery where balls are drawn for all the picks, rather than just the top 4.
  - Include a randomly selected wild-card playoff team and invite them to participate in the lottery.

- Simulate the 1985 “frozen envelope” NBA Draft Lottery, and explore the popular conspiracy among the NBA media and NBA fans that this event was rigged by the NBA.
  - Some background on this event: https://www.si.com/longform/2015/1985/ewing/index.html

![Screen Shot 2021-05-03 at 11 05 18 AM](https://user-images.githubusercontent.com/46533891/116901365-743b8500-abff-11eb-860a-b90d3544dfc5.png)

## Random Variables:

- The original NBA draft lottery can be translated to a Multinomial Distribution where every team is assigned a set of probabilities to land each of the 14 picks. 
  - N successive independent trials are performed for each team to see which of the outcomes is the most likely.
  - The results for each team are independent of each other because each trial contains only the odds for each team of getting picks #1-#14.

- The modified NBA draft lottery with the wild-card team can be modeled using a Normal Distribution with mean 0.07 and standard deviation 0.035.
  - The odds for the new playoff team will be determined from a random draw from this normal distribution
  - The odds for a randomly selected team in the bottom-5 of the league is adjusted down based on this result.

- The 1985 NBA Draft Lottery Conspiracy can be translated to the combination of a Bernoulli Random Trial + a Normal distribution.
  - First, a Bernoulli trial is performed (70% success/30% failure). This indicating whether or not the league gets caught trying to rig the lottery before it happens
    - If they do get caught (a failure result), the Knicks lottery odds are moved down to 0.01 the rest of the odds will be redistributed to the other teams
  - If they do not get caught, their odds are modeled as a normal distribution with a mean of 0.25 (representing their increased odds of winning the lottery versus other teams due to the "frozen envelope") and a large standard deviation of 0.1, illustrating that the result has high variability, since rigging the lottery is very risky (greatly increased odds, or only slightly increased odds of obtaining the number one pick).

