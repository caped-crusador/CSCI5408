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

```POST http://40.117.134.33:9200/bus/stops/_bulk```   and attach stops.JSON

```POST http://40.117.134.33:9200/bus_tr/trips/_bulk```   and attach trips.JSON

```POST http://40.117.134.33:9200/bus_stoptimes/stoptimes/_bulk```   and attach stoptimes.JSON


### Query 1
Part-1 

```POST http://40.117.134.33:9200/bus/stops/_search```

```json
{
  "query": 
        { 
        	"match_phrase": 
        	{ 
        		"name_stop": "south St [westbound] before I.w.k Hospital"
        	}
        }, "_source": ["stop_id"]
}
```
Part-2

```POST http://40.117.134.33:9200/bus_stoptimes/stoptimes/_search```
```json
 {
  "query": 
        { 
        	"match_phrase": 
        	{ 
        		"stop_id": "2026"
        	}
        }, "_source": ["trip_id"]
}
```
Part-3

```POST http://40.117.134.33:9200/bus_stoptimes/stoptimes/_search```
```json
{
  "query": 
        { 
        	"match_phrase": 
        	{ 
        		"trip_id": "6530560-2012_08A-1208BRsu-Sunday-01"
        	}
        }, "_source": ["trip_headsign"]
}
```
### Query 2

Part-1

```POST http://40.117.134.33:9200/bus_stoptimes/stoptimes/_search```
```json
{   "query": {  
    	"range" : {
        	"arrival_time" : {
            	"gte": "10:45:00", 
            	"lte": "11:00:00",  
            	"format": "HH:mm:ss"
        	}
    	}
	}, "_source": ["trip_id"]
}
```
One of the trip_id (6530560-2012_08A-1208BRsu-Sunday-01)is chosen from the output obtain from the query to get all the buses.

Part-2

```POST http://40.117.134.33:9200/bus_tr/trips/_search```
```json
{
	"query": {
		"match": {
			"trip_id": "6530560-2012_08A-1208BRsu-Sunday-01"
		}
	},
	"_source": "trip_headsign"
}
```
### Query 3

Part-1

```POST http://40.117.134.33:9200/bus_tr/trips/_search?q=route_id:FerD-116```
```json
{
  "query": 
        { 
        	"match_phrase": 
        	{ 
        		"trip_headsign": "1 SPRING GARDEN TO MUMFORD"
        	}
        },
  "_source": ["trip_id"]
}
```
Part-2

```POST http://40.117.134.33:9200/bus_stoptimes/stoptimes/_search```

```json
{
    "query" : {
        "match_phrase": {
           "trip_id": "6530560-2012_08A-1208BRsu-Sunday-01"
        }
    }, "_source": ["stop_id"]
} 
```
Part-3

```POST http://40.117.134.33:9200/bus/stops/_search```

```json
{   "query": {  
    	"range" : {
        	"stop_id" : {
            	"gte": "8327", 
            	"lte": "8328"
        	}
    	}
	}, "_source": ["name_stop"]
}
```
### Query 4
Part-1

```POST http://40.117.134.33:9200/bus_stoptimes/stoptimes/_search```

```json
{
	"size":0,
	  "aggs": {
	    "counts_stop_id": {
	      "terms": {
	        "field": "stop_id",
	        "order" : { "_count" : "desc" },
	    "size":3
	      }
	    }
	  }
}
```
Part-2

```POST http://40.117.134.33:9200/bus/stops/_search```
```json
{
	"query" : {
		"match" : {
				"stop_id":"8643"
		}
	}, "_source":["name_stop"]
}
```
Part-3

```POST http://40.117.134.33:9200/bus/stops/_search```

```json
{
	"query" : {
		"match" : {
				"stop_id":"8650"
		}
	}, "_source":["name_stop"]
}
```
Part- 4

```POST http://40.117.134.33:9200/bus/stops/_search```

```json
{
	"query" : {
		"match" : {
				"stop_id":"8655"
		}
	}, "_source":["name_stop"]
}
```
