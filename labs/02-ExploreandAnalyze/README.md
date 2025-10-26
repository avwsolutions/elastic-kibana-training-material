# Introduction lab exercises

Welcome to the Explore and Analyze with Kibana lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about the legendary Elastic Stack.

The goal is to get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- Elastic Kibana UI
- Working with Data views
- Collecting data
- Leveraging Elastic Integrations
- Introduction to Kibana Lens


## Exercise 1 - Exploring Global CyberSecurity Threats 2015-2024

This first exercise you are required to import the dataset, which we provide with this material.

The dataset is provided through [Kaggle](https://www.kaggle.com/datasets/hassaneskikri/ai-enhanced-cybersecurity-events-dataset). Here you will find more information about the content and technical specifications like CSV columns.

We already added the CSV download to this course material, which is named as [ai_ml_cybersecurity_dataset](./content/ai_ml_cybersecurity_dataset.csv).

Either choose one of the options to download the dataset.

### 1.1 - Import CSV data

- Open Home.
- Click on Add integrations.
- Search for CSV.
- Click Upload a file to open the window.
- Great, let's upload the [ai_ml_cybersecurity_dataset](./content/ai_ml_cybersecurity_dataset.csv).
- Everything seems well mapped, but we can correct things here.
- You can override settings, but keep them *default* for now.
- Click import.
- Ensure you have an unique index name starting with your login name like *'user1_cyberthreats'*.
- Now view and analyse this imported data set. 
- Do the events show up in Kibana? Can you temporary achieve this using the default created Data View?

Now answer the following questions:
- Can you create a filter to only see `Attack Type` of DDOS?
- Can you optimize the column that you only see the colums below, in order:
    - Timestamp.
    - Attack Severity.
    - Response Action.
    - Data Exfiltrated.

### 1.2 - Creating your own document list

Here you are going to apply your recently learned skills. Create a filter and ensure that only the requested data is shown.

- List all `source IPs` are responsible for `Attack Severity:Critical`.

Advice is to first create a filter, semantics follow later. You may want to save your `Discover Session`.

## Exercise 2 - Using Kibana Graph

This exercise you will get introduced in using `Kibana Graph`. Graph for short can be helpful analyzig dependencies and relationships. We are going to use the previously imported `cyberthreats` dataset.

### Exercise 2.1 - Import data into Kibana Graph

- Open Kibana.
- Open Graph, under Analytics.
- Create Graph.
- Select your recently created data view as data source
- Now you can add the following fields.
    - Attack Severity.
    - Attack Type.
    - Data Exfiltrated.
    - Response Action.
- Now click on Graph.

Now answer the following questions:
- First block any `Attack Type` of DDOS.
- Try to drill-down and disable some fields.
- What does the thickness of the lines suggest?
- Which `Attack Type` is the most active threat?

Take a moment to look through the Kibana Graph functionality.

## Exercise 3 - Introduction to Kibana Maps

This exercise you will get introduced in using `Kibana Maps`. Maps as you may expect can visualize country, city or other maps and map documents as data points. This exercise you get introduced in some functionality.

### Exercise 3.1 - Create your Maps dataset

- Open Dev Tools
- Create a new unique index like *'user1_maps-demo'*

```
PUT user1_maps-demo
{
  "mappings": {
    "properties": {
      "country": {
        "type": "keyword"
      },
      "location": {
        "type": "geo_point"
      },
      "name": {
        "type": "text"
      }
    }
  }
}
```
- Now add two documents. See examples below.

```
POST user1_maps-demo/_doc
{
  "name": "Utrecht Office",
  "country": "Netherlands",
  "location": 
  {
    "lat": 52.0907,
    "lon": 5.1214
  }
}

POST user1_maps-demo/_doc
{
  "name": "San Francisco Office",
  "country": "United States",
  "location": 
  {
    "lat": 37.7749,
    "lon": -122.4194
  }
}
```
- Now use search to see if the documents are succesfully ingested.

```
GET user1_maps-demo/_search
```

Now answer the following questions:
- Why are you using different field types?
- Explain how the location field is setup.

### Exercise 3.2 - Create a Data View

 Here we are going to create a simple `Data View`. 

 - Open Kibana.
 - Open Stack Management.
 - Open Data Views under Kibana.
 - Create Data View.
 - Name it `maps-demo`.
 - Index pattern your index name. So only one match !!!
 - Click save data view to kibana.

Now answer the following questions:
- Why can't you select a timestamp field?
- How can you match multiple indices?


### Exercise 3.3 - Open your maps-demo in Kibana Maps

This last exercise you are going to open the documents in Kibana Maps.

- Open Kibana.
- Open Maps under Analytics.
- Click Create Map.
- Click add Layer.
- Click Documents.
- Select your previously created data view.
- Save your Map.

Now answer the following questions:
- Can you search for a particular office like "San Francisco Office"?
- What if you remove the Basemap?

## Next Steps

You are ready to start with the third lab about [Kibana Search](../03-KibanaSearch/README.md) for Elastic Kibana. Be aware that the trainer might have to explain the training material and provide additional instructions for a jump start.

Enjoy the exercises!!!
