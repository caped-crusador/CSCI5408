# CSCI5408
## Assignment 1
### Task: To perform EalsticSearch on the Bus data of the Municipality of Halifax. 
In order to get started with this task, first of all we need to install the necessary packages and tools on the system.
Elastic search needs Java to perform its tasks, we neeed to add the rpository and install java on the system.

Open your terminal and type the follwing commands:

```sudo add-apt-repository -y ppa:webupd8team/java```
```sudo apt-get update```
```sudo apt-get -y install oracle-java8-installer```


Download and install the Public Signing Key:

```wget -qO - https://packages.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -```


Save the repository definition to /etc/apt/sources.list.d/elasticsearch-6.x.list:

```echo "deb https://artifacts.elastic.co/packages/6.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-6.x.list```


Now run apt-get update and the repository is ready for use. it can be installed with using the foloowing commands:

```sudo apt-get update && sudo apt-get install elasticsearch```

upload the data on the server to perform search on it
while performing the below mentioned queries, the body of the request needs to be populated with the data of the tables in JSON  

```POST http://40.117.134.33:9200/bus/stops/_bulk```   and attcah stops.JSON

```POST http://40.117.134.33:9200/bus_tr/trips/_bulk```   and attcah trips.JSON

```POST http://40.117.134.33:9200/bus_st/stoptimes/_bulk```   and attcah stoptimes.JSON


### Query 1
part-1 

```POST http://40.117.134.33:9200/bus/stops/_search```
_{
  "query": 
        { 
        	"match_phrase": 
        	{ 
        		"name_stop": "south St [westbound] before I.w.k Hospital"
        	}
        }, "_source": ["stop_id"]
}_

part-2

```POST http://40.117.134.33:9200/bus_st/stoptimes/_search```

_{
  "query": 
        { 
        	"match_phrase": 
        	{ 
        		"stop_id": "2026"
        	}
        }, "_source": ["trip_id"]
}_

part-3
```POST http://40.117.134.33:9200/bus_st/stoptimes/_search```


