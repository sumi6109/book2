# NetApp

Brian McKean from NetApp presented to the class a data analysis problem he'd
like to get some help on.

# Overview

Listen to his presentation carefully. Write down the answers to the following
questions to show your team's understanding of the basics of the problem.

## What is the problem?
Brian wants to track how the systems are being used and the system usage data is inconsistent.



## Why is the problem importnat?
Because it's important to have consistent and accurate information about how the systems are being used.



## What dataset has been made available?
Brian has provided a spreadsheet of the systems (not individual drives) and their observation times and information.



## What specific questions are being raised?
How many ASUPs can we use?

Can we identify patterns in the unusuable ones so that we can make them usable?

Are there patterns that can help us improve?

# Q/A session

We will run a Q/A session. Before the session, compile a list of questions you
want to ask. Then, teams will take turn to ask Brian follow up questions.
Each team gets to ask one question each time. Write down the questions your team
wanted to ask and the answers you received. If another team happens to ask the
same question, simply write down the answer you heard.

## If there are multiple entries for a particular system serial number, can you average those entires to determine usage information?

Yes. There are multiple records for particular systems and they are used to determine usage information.



## Can you get the expected value of writes to a drive over time to predict failure?

No. There could be a large number of writes initially or over some random short period of time that would skew data, since they cannot predict how customers will use the drives.



## If you have observation periods longer than 24 hours, can you assume that it is indicative of a normal 24 hour cycle (i.e., usage changing on weekends)?

There is a change in time calculated between the observation time and the base time for the system to account for this.




# Approach

Based on the information you've obtained during the Q/A session, come up with
plan how your team will tackle this problem.

## How should the dataset be imported into Tableau?
Because the data set is a csv, it can just be directly imported into Tableau.



## How should the work be distributed among the team members?

One team member per question.


## What types of charts or visualizations to use to support the answer?

We will evaluate what visualizations are the best upon importing the data.


## What questions may be too complex for Tableau and may require custom scripts to be written?
Questions that involve complex statistical analysis on the data would require more math than Tableau is capable of.
