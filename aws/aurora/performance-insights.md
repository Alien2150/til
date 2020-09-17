# Analyze querries step by step

* Goto Performance Insights. Choose the instance/timeframe when seeing load-impact
* Choose the query -> A download button will pop up
* Save the query ```exlain analyze <query>``` 
* Run ```psql -qAt -f <file> > analyze.json```
* Feed into Query Planner Visualizier: http://www.tatiyants.com/pev/#/plans/new
* Look for seq - scans. Consider using LATERAL Joins if possible
