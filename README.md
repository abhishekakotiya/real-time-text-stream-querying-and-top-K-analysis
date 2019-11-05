# Indexing & Searching for Most Frequent Topics with ElasticSearch, Apache Spark, Kafka, Count-Min, and Heavy Hitters

Top-K/heavy-hitter analysis and keyword based querying on live Twitter stream. The statistics on the collected keywords are dynamically updated.

### Approach
1. Make Twitter developer accounts to receive access tokens and keys for app.
2. Configure confluent to spawn all the required services (Zookeeper, kafka e.t.c)
3. Configure twitter source config file to get data form twitter and dump in Kafka topic.
4. Configure elastic search sink config file to transfer data from Kafka to elasticsearch.
5. Now data will be flowing from Twitter to Kafka to Elastic Search.
6. We split the tasks in 2 phases now:  

**Client to support various type of queries on elastic search**   
Made a user interface for performing various type of queries on the streaming twitter data which is now stored on the elastic search Term Query, Match Query, Prefix Query and Fuzzy Query  

**Stream data from Kakfa to calculate the heavy hitters periodically**  
We used Apache Spark to generate streams of tweets from Kafka and then
* NLTK to tokenize the stream of tweets into words
* Bloom Filters to quickly filter the stop words in the stream
* We updated the count min sketch for each word in the stream
* Calculated the Top K Heavy hitters using the sketch from the stream.
* Printed the Heavy hitters periodically

**Note**: Add your own access tokens and keys from your Twitter Developer Account in the empty strings in the **twitter-source-json.json** config file, to run this code.


For information related to Elasticsearch querying and implementation, refer ElasticsearchDocumentation.pdf

For instructions on setup and how to run this code, refer InstallandRunInstructions.pdf
