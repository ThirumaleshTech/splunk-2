># Total number of PCs imaged
-----


```
sourcetype="BDD" OR sourcetype="BDD-2" OR sourcetype="BDD-3" OR sourcetype="BDD-4" AND source="*" AND host="YOURINTENDEDHOST" | dedup source | stats count
```

##### Notes:
- Based on Windows MDT Log data for BDD.LOG file specified in the `\DeploymentShare\Logs\*\BDD.LOG` location where * represents the directory created for each client imaged by MDT.
- MDT Log data from (BDD.LOG) is sometimes imported into Splunk into multiple BDD source types an issue that I am still investigating. For now, this search utilizes all of those source types, any source file, and specifies a host for restricting results to a specific server.