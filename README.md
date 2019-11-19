# seatingLP
Same seating problem and more background available in https://github.com/jingweikang/seating. Sample data files are SampleCompanies.csv and SampleStudents.csv.

## Previous approach
Converted the previous code to Python in SimpleSeating.ipynb file. Sample output is in SampleSimpleFinal.xlsx file. Note how most participants have a high "satisfaction score", since the student preferences are processed on a first-come-first-serve basis. The last couple participants have a low score, since the tables of companies they prefer may already be full. 

The satisfaction score is just an arbitrary metric. If there are *n* companies on a student's preference list, I award *n* points for the student's first choice, *n-1* for the second choice, *n-2* for the third choice, etc. This score is then normalized so that for *r* rotations, the student has the maximum satisfaction score of *1* if he or she is seated with the top *r* preferences.

With this approach, the average satisfaction was 0.923 (out of 1), but there was a 0.778 difference between the most satisfied and least satisfied person, which is a significant difference. The sample output is in SampleSimpleFinal.xlsx.

## Linear programming approach
The above approach to seating is simple and iterative, which is how a human assigning seats would probably handle it. The next step is to formulate the problem as a linear programming problem, which can allow us to maximize the satisfaction scores of the population as a whole. We do this in SeatingLP.ipynb. By framing the problem as a LP problem, we can also have participation constraints; for example, if there are *r* rotations, a student must be seated with *r* companies. 

With the prior approach, we can see this isn't the case for the last couple of participants, where they perhaps sat with the least popular companies in early rotations and find that these are still the only available tables at later rounds (but they cannot sit with the same company twice so they are not assigned a company). With the prior approach, this would require us to manually swap seating assignments, which may be time-consuming and tricky. Linear programming would allow us to ensure that students are seated with a new company at each rotation. The exact constraints are below:

![alt text](https://github.com/jingweikang/seatingLP/blob/master/SeatingLPFormulation.png)

The sample output is in SeatingLPFinal.xlsx. Our average satisfaction improves to 0.974 (out of 1), and we reduce the difference between the most satisfied and least satisfied person to 0.167 (from 0.778).

## Prioritizing early responders
From looking at the sample output, we can see that we don't always prioritize the earliest responses. To address this, we can modify the objective function to prioritize the participants who submitted their preferences first. The relevant files are SeatingLPWithPriority.ipynb and SampleLPPriorityFinal.xlsx. Specifically, we multiply the satisfaction scores of each student by some function related to the position of their response. Determining this function isn't an exact science - it can determine significantly on the feasible region of your linear program (based on your constraints) as well as the objective function. As you might expect, doing so will increase the difference between the most satisfied and least satisfied person, but I was able to still have an average satisfaction higher than the iterative approach while also keeping our desired seating constraints. 
