# Introduction lab exercises

Welcome to the Kibana Visualize lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about the legendary Elastic Stack.

The goal is to get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- Visualizations exploration 
- Using Kibana Lens
- Using Kibana Maps
- Using Vega custom visualizations

## Exercise 1 - Analyse Web Logs

This first exercise you are going to analyse the sample web logs which are already loaded into an index for you.
During this exercise you will use `Kibana Lens` and improve your visualization with `Annotations` and `Reference` layers.

### Exercise 1.1 - Create insights on average bytes over time

Open Kibana Lens and ensure the index is using `Kibana Sample Data Logs` as Index View.

- Start with droppping the `Timestamp` field to Grid and choose the `Stacked Bar` visualization.
- Adjust the Y-Axis to `Average of bytes field`.

<img src="https://github.com/avwsolutions/elastic-kibana-training-material/blob/main/labs/04-KibanaVisualize/content/example11.png?raw=true" alt="example 1-1">

### Exercise 1.2 - Add failed request markers for HTTP errors

We are going to continue with our previously created visualization and additional `Annotation`, which will be used to mark and easily identify HTTP Errors, in-specific we are looking for `HTTP Error: 503`.

- Start with adding an additional layer and select the `Annotations` type.
- Choose `New annotation`. Now click the added Event annotation to start the configuration.
- Choose custom query and set the KQL query to `response: 503`.
- Change the name to `HTTP Error`.
- Change the icon to a `bolt`.
- As tooltip add an additional field called `clientip`.
- Don't forget to save the visualization to your library for later usage.

<img src="https://github.com/avwsolutions/elastic-kibana-training-material/blob/main/labs/04-KibanaVisualize/content/example12.png?raw=true" alt="example 1-2">

Now answer the following questions:
- What do you see when you hover the annotation?
- Explain why sometimes the icon is not shown.
- Can you think of another use case when annotations can be helpful?

### Exercise 1.3 - Add the expected baseline for average bytes usage

In most scenarios you always have a baseline or a reference value. This helps us to easily see deviations from our baseline.
During this exercise you are going to configure a `Reference value`.

- Start with adding an additional layer and select the `Reference value` type.
- Choose a `Data View`. Now click `add a field`.
- For method choose `Formula` and set this to `average(bytes, kql='response=200')`.
- Change the name to `Expected baseline`.
- Change the value format to `bytes`.
- Change the icon to a `tag`.
- Don't forget to save the visualization to your library for later usage.

<img src="https://github.com/avwsolutions/elastic-kibana-training-material/blob/main/labs/04-KibanaVisualize/content/example13.png?raw=true" alt="example 1-3">

Now answer the following questions:
- Explain why a Formula differs from a static value.
- Can you think of another use case when references can be helpful?

## Exercise 2 - Using Geospatial data in Kibana Maps

This exercise you will learn another great feature of using `Kibana Maps`. You are going to load `Geospatial data`, such as a `Geo JSON` formatted input file.

### Exercise 2.1 - Load a Geo JSON file as layer

Some use cases it's great to load a company specific map with store locations or other important geographical areas. Nowadays a lot of Geo data is publically available.  For example the indeling of `Amsterdam`, which is available in `Geo JSON` format. Let's load this into Kibana Maps and solve some questions.

- Open Maps under Analytics.
- Click Create Map.
- Click add Layer.
- Click Upload file.
- Choose [indelingamsterdam.json](./content/indelingamsterdam.json)
- Use an unique index name like `user1_amsterdam`.
- Click `Add as document layer`.
- Save your Map.

Now answer the following questions:
- Can you create a query to display for `Stadsdeel` Zuid?
- Can you display both display `Stadsdeel` Zuid en Noord? 
- Which stadsdeel is bigger?

### Exercise 2.3 - Bous Load Flight destinations on Heat map

This bonus exercise let you load another type of `Maps visualization` using a Heat map. Here we will use the `Flight data`.

- Open Maps under Analytics.
- Click Create Map.
- Click add Layer.
- Choose Heat map.
- Select the `Kibana Sample Data Flights` Data View.
- Choose either `Destlocation` or `originLocation`.
- Keep changes and continue.
- Fill-in an unique name.

Ensure that the `query` bar is empty and lookup the cities.

Now answer the following questions:
- Which cities do you see?
- Which city has the most flights?

## Exercise 3 - First experience with coding Vega

This exercise you will learn the basics about Vega. Vega is a powerful way of  building dashboards, but can be development heavy especially for non-developer users. You are going to load an example configuration and adjust this for your needs.

### Exercise 3.1 - Create a simple Vega-lite example

We are going to create a custom visualization using Vega.

- Open Visualization library under Analytics.
- Click Create Visualization.
- Choose custom Visualization.
- Save the boilterplate code for now using a unique visualization name.
- Now change the title to `My first Vega experience`.
- Use the previously created index called `user1_cyberthreats`.
- Fix the timestamp fields (two times) and ensure the timepicker has set for minimum 5 years.
- Click update to see the results.

Now answer the following questions:
- What are the benefits using Vega?
- Which use cases would you apply this?

### Exercise 3.2 - Load the ecommerce demo

This exercise you are going to load the ecommerce demo. The JSON content is already available under [vega-example](./content/vega-example.json)

 Open Visualization library under Analytics.
- Click Create Visualization.
- Choose custom Visualization.
- Clear the code field.
- Copy/paste the content of [vega-example](./content/vega-example.json).
- Use reformat if needed.
- Click update to see the results.

Now answer the following questions:
- Discover the differences with the previous example.

## Next Steps

You are ready to start with the fourth lab about [Kibana Sharing](../05-KibanaSharing/README.md) for Elastic Kibana. Be aware that the trainer might have to explain the training material and provide additional instructions for a jump start.

Enjoy the exercises!!!
