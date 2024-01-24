## Eventual Consistency

Enter Eventual Consistency - It’s at this point in my career that I discovered that **services can maintain a copy of other services’ data, locally in their own DB tables.** It comes with the responsibility to retain that data via events or polling.

Included in this package is the fact that the data may be stale for some time, but that it’ll eventually be updated, meaning the data is eventually consistent. We can’t guarantee that the data isn’t stale, but we can guarantee that we’ll eventually catch up.

The moment it “clicked” for me was when I thought about it from the perspective of a backend service depending on a public weather API for weather data. Instead of retrieving weather data for Prishtina or Berlin every time a user from those respective cities needs weather data, I cache it (maybe multiple times a day) by materializing it in a local table and serving cached data to those users. I’ve made the trade-off in favor of eventual consistency because it’s not crucial for my users to see the freshest data, it’s OK if it’s a few hours stale.

Going back to the Challenge example: we can cut off many synchronous dependencies to the User service by just maintaining a local copy of users in the services:

- Leaderboard service can maintain a local copy of users and avoid having to make requests to User service. No one really minds if the data is a bit old, it’s not a showstopper if someone sees a slightly old avatar.
- Challenge service can do the same; say if it exposed a getChallengeDetails query and needed user display names and avatars to show the current challenge participants — it can also serve this eventually consistent data from its own materialized users table.
- Notification service, although a bit more sensitive, can also utilize data sharing to remove its dependency on the Users service. It can materialize users locally and maintain a best-effort updated state by listening to User updated events to ensure it has the most up-to-date emails.

Although we didn’t talk much about how services share this data (a topic for another time), a final example architecture would make use of a combination of event sourcing and caching. Here’s a sneak peek into what this kind of architecture would look like:

![image](https://github.com/AdyKalra/technolgytrends/assets/8856857/ea89ac6c-2094-4bbe-a03f-c66653e7447d)


Example architecture with two main methods of sharing data between services: event sourcing and caching
If you want more examples, take a look at [How to Share Data Between Microservices on High Scale by Shiran Metsuyanim](https://medium.com/fiverr-engineering/how-to-share-data-between-microservices-on-high-scale-ab2bc663898d), an engineer at Fiverr. It’s a great post that shows how to maintain robustness when adding a new service. It starts out by laying down the constraints, and then discussing the trade-offs between synchronous, asynchronous, and hybrid solutions.
