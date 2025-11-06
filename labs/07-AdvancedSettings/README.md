# Introduction lab exercises

Welcome to the Advanced setting lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about the legendary Elastic Stack.

The goal is to get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- Kibana Advanced settings
- Elasticsearch Advanced settings
  - Runtime fields using `Painless`
  - Enrichment policies using `Ingest Pipelines`

### Exercise 1 - Exploring and understanding Kibana Advanced Settings

### Exercise 1.1 - Changing an Kibana Advanced Setting

Many developers like to work at night. This requires Kibana by default using the `Dark mode` within your `personal Space`.  Your colleagues asked you to configure this.

- Open Kibana.
- Open Stack Management.
- Click Advanced Settings under Kibana.
- Run the following statement.

Now answer the following questions:
- Did you need to logout or restart Kibana to activate this setting?
- Can you configure this cluster-wide?
- Find the default index for `Elastic Security` TI indices.
- Which settings do you find under `Notifications`.

## Exercise 2 - Adding a Runtime field which uses Painless

This example you are creating a `Runtime field`, which dynamically creates a new field at runtime. We are going to use this to add a `CI Identifier`to our incoming `logs`.

To achieve this we are going to extend `logs@custom`.

- First add the object called `user1`. This wil be the placeholder.
- Create a runtime field called user1.system_id as type KEYWORD
- Add the *Painless* script below.

```
String systemId = "CI_" + doc['host.name'].value.toUpperCase() + "_X001";
if (systemId != null) emit(systemId);
```

Ensure that you did a rollover to activate the runtime field. Take notice that `logs@custom` impacts all data streams that start with 'log-*'. 

Below the steps to activate.

- Open Dev Tools
- POST <datastream>/_rollover

## Exercise 3 - Creating an Ingest Pipeline for Asset Enrichment

This exercise we are going to enable enrichment on our logs based on the `host.name`. Ensure that you carefully read the instructions, since this requires multiple steps to succeed. Additionally ensure that the `docker-elastic-agent` is healthy under `Fleet Management`.

### Exercise 3.1 - Add the initial asset table

```
PUT /user1_assets/_doc/1?refresh=wait_for
{
  "name": "docker-elastic-agent",
  "description": "Lab environment Dockerized Elastic Agent",
  "owner": "<your-fake-name>",
  "score": "100",
  "unit": "training"
}
```

### Exercise 3.2 - Add the initial asset-policy for enrichment

```
PUT /_enrich/policy/user1-asset-policy
{
  "match": {
    "indices": "user1_assets",
    "match_field": "name",
    "enrich_fields": ["name", "description", "owner", "score" ]
  }
}
```

### Exercise 3.3 - Enable the asset-policy

```
POST /_enrich/policy/asset-policy/_execute?wait_for_completion=false
```

### Exercise 3.4 - Create an asset_lookup pipeline

```
PUT /_ingest/pipeline/user1_asset_lookup
{
  "processors" : [
    {
      "enrich" : {
        "description": "Lookup assets",
        "policy_name": "user1-asset-policy",
        "field" : "host.name",
        "ignore_missing": true,
        "target_field": "user1-asset",
        "max_matches": "1"
      }
    }
  ]
}
```

### Exercise 3.5 - Extend Elastic Agent Normalization with asset enrichment

```
PUT _ingest/pipeline/logs@custom
{
  "processors": [
    {
      "pipeline": {
        "name": "user1_asset_lookup",
        "ignore_missing_pipeline": true,
        "tag": "enrich"
      }
    }
  ]
}
```

### Exercise 3.6 - Test enrichment and look if assets are enriched

- Open Kibana console
- Filter for host.name: specific event.
- Look if the specific host events are enriched.
- Try to add another asset entry to enrich.

## Next Steps

You have successfully completed all labs for the Elastic Kibana training course. You are now ready to enter the real world and create awesome Kibana dashboard!

Enjoy the Elastic Stack!!!
