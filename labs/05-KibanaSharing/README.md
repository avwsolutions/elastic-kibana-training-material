# Introduction lab exercises

Welcome to the Kibana Sharing lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about the legendary Elastic Stack.

The goal is to get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- Understanding ES|QL
- Building dashboards
- Sharing dashboards
- Automatic reporting
- Alerts and notifications

## Exercise 1 - ES|QL Queries for fun, analysing Web logs

This first exercise you are going to play around with ES|QL, which is a new Elastic Query Language. We keep things easy. Let's start!

### Exercise 1.1 - Open the ES|QL Console and show the last 10 events

- Open Kibana, Discover
- Click top-right on Try ES|QL

Now get the last 10 events from `kibana_sample_data_logs`.

### Exercise 1.2 - Create a query that counts all events last 30 seconds

- Query must be in ES|QL.
- Query must be piped over multiple lines for readability.
- Ensure you use STATS function.

```
FROM kibana_sample_data_logs
| WHERE @timestamp > NOW() - 30 second
| STATS COUNT(*)
```

Explain why result is '0' and now try for the last 30 day?

### Exercise 1.3 - Query events where host.name start with docker and show the total_events per agent.name

- Query must be in ES|QL.
- Query must be piped over multiple lines for readability.
- Ensure that DESC is selected.

Try out the query. Which agents are shown?

- Examine the output.
- Review the query and look if you can play around with changing the WHERE clause.

```
FROM logs-*
| WHERE host.name LIKE "docker*"
| STATS total_events = COUNT() BY agent.name
| KEEP agent.name, total_events
```

### 1.4 - Parse a log based on an advanced workflow

- Query must be in ES|QL.
- Query must be piped over multiple lines for readability.

Which advanced workflow will you use? 

Either GROK or DISSECT. You get the DISSECT for free, now you have to develop the GROK code snippet.

```
ROW logentry = "2025-06-02T12:15:00.000Z - ghost - 192.168.30.1"
| DISSECT logentry """%{@timestamp} - %{host.name} - %{ip.address}"""
| KEEP @timestamp, host.name, ip.address
```

### 2.5 - Create a list of of certified movies

- Query must be in ES|QL.
- Query must be piped over multiple lines for readability.
- Query must extract only the main Genre.
- Query must extract only the year.
- Results must be sorted by ASC.
- Query must output year, main Genre, Title, Rating.

Can you create a query this query from scratch? You can load the data records from [movies.csv](./content/movies.csv). Ensure you map `Year` to the correct `field type` called `date`.

- Examine the output.
- Review the query and look if you can change this for other processes.

```
FROM MOVIES
| GROK Genres "%{WORD:MainGenre}"
| EVAL year = DATE_EXTRACT("year", Year)
| SORT Rank ASC
| WHERE Certificate LIKE "PG*"
| KEEP year, MainGenre, Title, Rating
```

## Exercise 2

This exercise you are going to build a dashboard which visualizes `IMDb Top 250 Movies` you have loaded in the previous exercise.
The goal is to create a fully functional dashboard that provides insights and helps to analyze all your favorite movies.

<img src="https://github.com/avwsolutions/elastic-kibana-training-material/blob/main/labs/05-KibanaSharing/content/example_dashboard.png?raw=true" alt="example dashboard">

Look to the dashboard above for inspiration and how it could look like.

### Exercise 2.1 - Create the initial dashboard

this exercise you are going to create the initial dashboard that must met the following requirements.

- Create a new dashboard and give it an unique name like `user1_IMDb Top 250 Movies`.
- Add three `Collapsible sections` called from top to botomm
    - Overall Analysis
    - Actionable Insights
    - Involved Documents
- Ensure it has an unique personal tag like `user1`.
- Ensure the `timepicker` is set to `110 years`.
- Now save the dashboard.

### Exercise 2.2 - Add the involved documents panel

this exercise you are going to create a `Discover Session` that must met the following requirements.

- Open a new Discover tab.
- Ensure you have selected your `movies` index. 
- Add the following columns.
    - Year
    - Rank
    - Title
    - Description
    - Movie URL
- Now ensure that `Year` only shows `YYYY`, which can be done using `edit data view field`.
- Ensure the documents are **only** sorted by `Rank`.
- Save the `Discover session` as an unique search called `[user1] Included movies`.

Now open your previously created dashboard and add the `Discover Session` under the `Involved Documents` section. Ensure that the width spans the whole grid.

### Exercise 2.3 - Add the Overall Analysis section

this exercise you are going to create a `Lens based visualization` that must met the following requirements.

- Open a new Kibana Lens session.
- Ensure that X-Axis is `Date histogram` on field `Year` with a minimal interval of `1y`.
- Ensure that Y-Axis is `Average`on field `Rating`. Ensure name show `Average of Rating`.
- Add a first `Annotations` layer to show not certified movies using a `KQL` query.
- Use the following query `Certificate :"N/A"  or Certificate : "Not Rated"`
- Ensure name is set to `Not Certified movie` and use the `Alert`icon.
- Show the `Certificate`field as tool tip.
- Now add a second `Reference lines` layer with name `Minimal rate`. 
- We use a `static value`of 8,5 as `Refence line value`.
- Ensure the line is `2px` and uses `red` as color. You may want to add an `icon`.
- Save this visualization direct to your dashboard as `[user1] Average rating of Movies`.

Move the visualization under the `Overall Analysis` section and Don't forget to save the dashboard.

### Exercise 2.4 - Add the Actionable Insights section

Here we keep things simple. Just add two visualizations;
- One Pie chart which shows the `Top 10 Genres`.
- One Metric which shows the `Highest Rank`.

- Open a new Kibana Lens session.
- Create Pie by adding `Genres`.
- Use `Top values`.
- Maximum `10` values and no `others`.
- Rank by `count of records`.

- Create Metric by adding `Ranking`.
- Use `Mininmum` function on `Ranking`.
- Fix the appareance that it shows a large `number` which is centralized in the middle.

### Exercise 2.5 - Add documentaton part

Now let's add the documentation section, which you add a `Markdown` panel that shows the `Usage instructions` to the left. Additional you download your favorite picture and this as `Image` panel to the right. Use your own idea how to format the `instruction`and `image`. Ensure that the new `Documentation section`is at the top.

### Exercise 2.6 - Make your dashboard interactive by using controls

Last part you need to make the dashboard more `interactive` using `Controls`. Here we are going filter on `Rating` with a `Range Slider` which we call `Select Rating`. 

Second we choose `Certification` with a `Options list`, which we call `Select Certification`.

Now don't forget to save your dashboard.

### Exercise 2.7 - Add a bonus Wordcloud

As bonus you can add an additional Wordcloud with `Movie URL` to the `Actionable Insights` section.

## Exercise 3 - Share your awesomeness

This exercise is all about sharing your results.  It's always good to share results.

- Share your dashboard link with all course mates using the `Dashboard Share` button.
- Export a report in `PNG` format and mail this to your trainer.

## Next Steps

You are ready to start with the fourth lab about [Stack Administration](../06-StackAdministration/README.md) for Elastic Kibana. Be aware that the trainer might have to explain the training material and provide additional instructions for a jump start.

Enjoy the exercises!!!
