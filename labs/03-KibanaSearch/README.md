# Introduction lab exercises

Welcome to the Kibana Search lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about the legendary Elastic Stack.

The goal is to get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- Elasticsearch as search engine
- Basic querying DSL and filtering
- Working with Kibana Query Language
- Understanding aggregations

## Exercise 1 - Exploring Driver Licenses

This first exercise you are required to import the dataset, which we provide with this material.

We already added the CSV download to this course material, which is named as [driverlicenses](./content/driverlicenses.csv).

### 1.1 - Import CSV data

- Open Home.
- Click on Add integrations.
- Search for CSV.
- Click Upload a file to open the window.
- Great, let's upload the [driverlicenses](./content/driverlicenses.csv).
- Everything seems well mapped, but we can correct things here.
- You can override settings, but keep them *default* for now.
- Click import.
- Ensure you have an unique index name starting with your login name like *'user1_driverlicenses'*.
- Now it's important to adjust the mapping under advanced for the `name` field to `text`.

```
    "name": {
      "type": "text"
    }
```

- Now view and analyse this imported data set. 
- Do the events show up in Kibana? Can you temporary achieve this using the default created Data View?

### 1.2 - Exploring the data set using KQL

Here you are going to apply your recently learned skills. You are going to query data using KQL, which is the default search language.

Now answer the following questions:
- What responses do you get when searching for `NL` and `nl`. 
  - Are there any differences?
  - Can you explain them?
- Try the same for `Thomas` and `thomas`.
- Filter that you only see documents from the `country: US`.
- Filter for only the documents that are from `Arnold` and `Tim`.

## Exercise 2 - Using DSL Queries

This exercise you will get introduced in using `DSL Queries`. DSL Queries are executed through `Dev Tools` or added to the filters. We are going to use the previously imported `driverlicenses` dataset.

### Exercise 2.1 - Write a simple query

- Open Kibana.
- Open Dev Tools.
- Now create a `Match query` that only matches `zach` records.
- Extend the query that it also includes `thomas`.
- Now copy/paste the query part to create a `Filter` in `Kibana` and saves this as `DE candidates`.

Now answer the following questions:
- How do you use the filter to exclude the matched documents?

### Exercise 2.2 - Quering Sample Flight Data

Let's create another query, but now we are using the `Sample Flight Data` dataset.

```
GET kibana_sample_data_flights/_search
{
  "size": 3,
  "query": { "match": { "Carrier": "Kibana Airlines" } }
}
```
Now answer the following questions:
- How many documents are hit?
- How many documents are shown?


### Exercise 2.2 - Optimizing with a DSL Bool Query

Now we are going to optimize our previous query. We only want to see a certain document.

- Filter that we only have flights with destination Japan.
- Destination weather must not be Sunny, we only love Cloudy.
- Flight should not take off from the United States.
- Result must be one document only instead of default 10.

Below a boilerplate to start with.

```
GET kibana_sample_data_flights/_search
{
  "query": {
    "bool": {
      "must": {
      },
      "filter": {
      },
      "must_not": {
      },
      "should": {  
      }
    }
  }
}
```

Now answer the following questions:
- How many documents are hit?
- Which country did we origin from?
- What is the destination weather?

## Exercise 3 - Apply some statistics using Aggregations

### Exercise 3.1 - Find the average drivers age

Here we are using our previous imported dataset called `driverlicenses`.

Below the example aggregation that shows the `average` age of all drivers. Which is a `Metric Aggregation`.

```
POST user1_driverslicenses/_search
{
  "size": 0,
  "aggs": {
    "average_age": {
      "avg": { "field": "age" }
    }
  }
}
```

Create a Aggregation query that calculates the `average` age only of drivers that life in the `US`. 

### Exercise 3.2 - Calculate the average age per country

Here we are using our previous imported dataset called `driverlicenses`.

Below the example aggregation that shows the `average` age of all drivers. Which is a `Bucket Aggregation`.

Use the previous example aggregation as input. For bucket aggregation you may want to use a `terms`.

Create a Bucket Aggregation query that calculates the `average age` per `country`. 

### Exercise 3.3 - Visualize your aggregation using Kibana Lens

Now it's time to recreate the `average age per country` using Kibana Lens. 

- Open Kibana.
- Click on Visualize Library under Analytics.
- Ensure that you use the correct Data View.
- Select the visualization type.
- Ensure you have the correct aggregation configured for the X-Axis and Y-Axis.

### Exercise 3.4 - BONUS Improve the aggregation to sort on count of categories

Now let's improve our previous bucket aggregation by adding a sort, which is based on the number of `categories` per country.
Sorting must be Ascending. 

## Next Steps

You are ready to start with the fourth lab about [Kibana Visualize](../03-KibanaVisualize/README.md) for Elastic Kibana. Be aware that the trainer might have to explain the training material and provide additional instructions for a jump start.

Enjoy the exercises!!!
