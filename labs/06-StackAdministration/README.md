# Introduction lab exercises

Welcome to the Stack Administration lab exercises. During the lab exercises the student will experiential work through various tasks and activities to gain practical experience and develop new skills. In hands-on learning, attendees are given the opportunity to explore, experiment, and discover knowledge for themselves about the legendary Elastic Stack.

The goal is to get actively engage and ask questions if something is not clear or you are blocked. Important to understand that there are no strong dependencies between labs, so it's okay if you're behind and follow your own pace.

The following key topics are part of these exercises:

- User and roles
- Working with Spaces 
- Machine Learning
- AI Assistant

## Exercise 1 - Setup your personal Space

### Exercise 1.1 - Create an unique Space called user1

- Open Stack Management under management.
- Under Kibana open Spaces.
- Click create space.
- Add a space called *User 1 Personal Space*.
- Allow all solutions.
- Create space.

### Exercise 1.2 - Create a role called user1_space

- Open Stack Management under management.
- Under Security open Users.
- Click create role.
- Add a role `user1_space` with index privileges to **only your personal data views**, say `user1*` with privileges read, write and view_index_metadata.
- Give it access to the newly created space and all access for features available.
- Assign role.
- Close with create role.

### Exercise 1.3 - Create your personal testuser called testuser1

- Open Stack Management under management.
- Under Security open Users.
- Click create user.
- Add a user called `testuser1` with a secure password, Wilkomme1.
- Give it the `user1_space` role.
- Create user.

### Exercise 1.4 - Test Space access

Now open an Incognito browser and login into Kibana with your test user called `testuser1`. Now explore and look if all dashboards are working as expected. 

### Exercise 2 - Creating a Simple Machine Learing job

This exercise you are going to create a `simple` ML Job.  Just follow the steps below to create it using `kibana_sample_data_logs` data set.

- Open Kibana
- Click Machine Learning under Analytics
- Click Create Anomaly detection Job
- Select `kibana_sample_data_logs` 
- Choose `Categorization`.
- Use `Full data`, next.
- Use `Count`, select `message`, next.
- Give the job an unique ID like `user1-first-ml-job`, next.
- After a succesful validation, click next again.
- Take a moment to look into the `Summary` and `Create Job`.

Now `View Results` and answer the questions below:

- What is the maximum Anomaly score ?
- Which `Timestamps` have a Anomaly score of `1`?
- Can you find the records where `177.111.217.54` is mentioned?

## Next Steps

You are ready to start with the fourth lab about [Advanced Settings](../07-AdvancedSettings/README.md) for Elastic Kibana. Be aware that the trainer might have to explain the training material and provide additional instructions for a jump start.

Enjoy the exercises!!!
