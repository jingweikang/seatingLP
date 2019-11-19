# seatingLP
Same seating problem and more background available in https://github.com/jingweikang/seating. 

## Previous approach
Converted the previous code to Python in SimpleSeating.ipynb file. Sample output is in SampleFinal.xlsx file. Note how most participants have a high "satisfaction score", since the student preferences are processed on a first-come-first-serve basis. The last couple participants have a low score, since the tables of companies they prefer may already be full. 

The satisfaction score is just an arbitrary metric. If there are *n* companies on a student's preference list, I award *n* points for the student's first choice, *n-1* for the second choice, *n-2* for the third choice, etc. This score is then normalized so that for *r* rotations, the student has the maximum satisfaction score of *1* if he or she is seated with the top *r* preferences. 

## Linear programming approach
The above approach to seating is simple and iterative, which is how a human assigning seats would probably handle it. The next step is to formulate the problem as a linear programming problem, which can allow us to maximize the satisfaction scores of the population as a whole. Furthermore, this can allow us to have participation constraints; for example, if there are *r* rotations, a student must be seated with *r* companies. 

With the prior approach, we can see this isn't the case for the last couple of participants, where they perhaps sat with the least popular companies in early rotations and find that these are still the only available tables at later rounds (but they cannot sit with the same company twice so they are not assigned a company). With the prior approach, this would require us to manually swap seating assignments, which may be time-consuming and tricky. Linear programming would allow us to find an optimum seating assignment for the population, and we could modify the objective function to prioritize the participants who submitted their preferences first.
