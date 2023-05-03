 [![Gitter](https://img.shields.io/badge/Available%20on-Intersystems%20Open%20Exchange-00b2a9.svg)](https://openexchange.intersystems.com/package/intersystems-iris-dev-template)
 [![Quality Gate Status](https://community.objectscriptquality.com/api/project_badges/measure?project=intersystems_iris_community%2Fintersystems-iris-dev-template&metric=alert_status)](https://community.objectscriptquality.com/dashboard?id=intersystems_iris_community%2Fintersystems-iris-dev-template)
 [![Reliability Rating](https://community.objectscriptquality.com/api/project_badges/measure?project=intersystems_iris_community%2Fintersystems-iris-dev-template&metric=reliability_rating)](https://community.objectscriptquality.com/dashboard?id=intersystems_iris_community%2Fintersystems-iris-dev-template)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat&logo=AdGuard)](LICENSE)
# issue with load data


## how to reproduce

Open IRIS Terminal and run:
IRISAPP>w ##class(community.csvgen.generated.home202305032).ImportData()

Then open any SQL Manager and run the SQL:
```
SELECT actor,message,severity,sqlcode
FROM %SQL_Diag.Message
WHERE diagResult =
  (SELECT TOP 1 resultId
  FROM %SQL_Diag.Result
  ORDER BY resultId DESC)
```
You should see the error:

actor	message	severity	sqlcode
server	{"resultid":"1","bufferrowcount":500,"queuesize":2,"statistics":false,"from":{"file":{"file":"/home/irisowner/irisdev/data/Educational_Attainment_small.csv","columns":["Name","Year","Variable","Value","GeographyType","DateField","Location"],"header":true,"types":[12,4,12,2,12,11,12],"columnseparator":",","lineseparator":"\n"},"select":["Name","Year","Variable","Value","GeographyType","DateField","Location"],"intotypes":[12,4,12,2,12,11,12]},"into":{"table":"community_csvgen_generated.home202305032","hints":"","columns":["Name","Year","Variable","Value","GeographyType","DateField","Location"],"types":[12,4,12,2,12,11,12],"values":["Name","Year","Variable","Value","GeographyType","DateField","Location"],"jdbc":{"threads":4}}}	info	0
FileReader	Reader Complete: Total Input file read time: 19 ms,	completed	0
JdbcWriter	[SQLCODE: <-104>:<Field validation failed in INSERT>] [%msg:<Field 'community_csvgen_generated.home202305032.DateField' Invalid Sybase Date String format: Not valid day! Unparseable date: "12/31/2015 12:00:00 AM">]	error	-104
JdbcWriter	[SQLCODE: <-104>:<Field validation failed in INSERT>] [%msg:<Field 'community_csvgen_generated.home202305032.DateField' Invalid Sybase Date String format: Not valid day! Unparseable date: "12/31/2014 12:00:00 AM">]	error	-104
JdbcWriter	Writer Complete: Total write time: 30 ms,	completed	0
5 row(s) affected



