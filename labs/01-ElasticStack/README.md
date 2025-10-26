# Introduction lab exercises

Welcome to the Elastic Introduction lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about the legendary Elastic Stack.

The goal is to get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- Training resources
- Training setup & deployment
- Managing the Stack

## Exercise 1 - Downloading training resources

This first exercise you are required to download the training resources. You only need to download one package.

Most simply way is using Curl or [Download the ZIP](https://github.com/avwsolutions/elastic-kibana-training-material/archive/refs/heads/main.zip) using your favorite browser. Git is not part of this course, but we encourage using the Git client, which you can [download](https://git-scm.com/downloads/guis) for free.

Either choose one of the options to download the training material.

### 1.1 - Download using Curl

First the lab material and second the Second the deployment code.

```
cd
curl -L https://github.com/avwsolutions/elastic-kibana-training-material/archive/refs/heads/main.zip -o elastic-kibana-training-material.zip
unzip elastic-kibana-training-material-main.zip
mv elastic-kibana-training-material-main elastic-kibana-training-material
```

### 1.2 - Download using Git

```
cd
git clone https://github.com/avwsolutions/elastic-kibana-training-material.git
```

If you want to know more about Git, the Version Control System just visit the [Git-SCM Website](https://git-scm.com/).

Now that you have downloaded the material (and extracted the ZIP file) you may want to look into this directory.

```
cd ~/elastic-kibana-training-material
ls
```

## Exercise 2 - Getting Started

This exercise you will get started with Kibana. You will login into the Kibana environment which is available for the training. You may already got the `URL` and `student` credentials. 

Take a moment to look through the `training-setup` and try to discover all components. You may find out the deployed `version`.

### Exercise 2.1 - Login into Kibana

Open the `URL` with a modern browser like Chrome, Edge or Firefox. Ensure that you include the `Kibana Port`, which is `5601`.

At the Kibana login page you can type in your `Username` and `Password`.

<img src="https://github.com/avwsolutions/elastic-kibana-training-material/blob/main/labs/01-ElasticStack/content/login.png?raw=true" alt="login">

When you successfully logged in you will see the following page appear, which is `Home`.

<img src="https://github.com/avwsolutions/elastic-kibana-training-material/blob/main/labs/01-ElasticStack/content/home.png?raw=true" alt="kibana-home">

### Exercise 2.2 - Find Elastic Stack version

Now that are are logged in you can help us find the deployed version. Question yourself where this could be located. Just look around and you may find it somewhere in a top corner. Note the results for later usage.

 ## Exercise 3 - Quick Architecture primer 

You have learned about the `Elastic Stack` architecture we have used for the training setup. Let's learn more about the concepts behind.

*Concepts explained:*
 - Elasticsearch - Is the document store, which is a distributed JSON database.
 - Index - Is where the actual data is stored like a mini-database.
 - Fleet - Is where the deployed `Elastic Agents` are managed. Elastic Agents collect and ingest the actual data into the `Elastic Stack`.


<img src="https://github.com/avwsolutions/elastic-kibana-training-material/blob/main/labs/01-ElasticStack/content/training-setup.png?raw=true" alt="training-setup">


### Exercise 3.1 - Request the current Cluster health

Maybe you have heared of `Dev Tools`. This is a very helpful tool to query both `Elasticsearch` and `Kibana` APIs like a developer. Let's start this exercise.

- Open Kibana.
- Open Dev Tools under Management. You may want to skip the tour for now.
- Run the following statement.

```
GET _cluster/health
```

Now answer the following questions:
- What is the current state?
- What state colors are supported by Elasticsearch?
- What could be the potential issue here?
- Which API call is equivalent for looking up the cluster health?

### Exercise 3.2 - Lookup the current indices

We will stay using `Dev Tools` to explore the architecture. Let's look into the currently created indices.

 Run the following statement.

```
GET _cat/indices
```

Now answer the following questions:
- Note which indices or index are in `yellow` state.
- Try to filter out only the `kibana` indices using an asterix.
- Add the column names (append with `?v`) to the previous query to complete this exercise.

You may want to close this exercise by exploring other `Dev Tools` features using Help.

### Exercise 3.3 - Lookup the deployed agents

We will now return to `Kibana home`.  Here we start looking for `Fleet`, either using the `search bar` or instruction below.

- Open Kibana.
- Open Fleet under Management.

Now answer the following questions:
- Note which agents are registered.
- Note which function both agents fulfill. 
- Lookup which `Integrations` are activated using the assigned `Agent Policy`.

## Next Steps

You are ready to start with the second lab about [Explore and Analyze using Kibana](../02-ExploreandAnalyze/README.md) for Elastic Kibana. Be aware that the trainer might have to explain the training material and provide additional instructions for a jump start.

Enjoy the exercises!!!
