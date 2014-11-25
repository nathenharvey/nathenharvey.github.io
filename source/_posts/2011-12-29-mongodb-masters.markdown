---
layout: post
title: "MongoDB Masters"
date: 2011-12-29 13:46
comments: true
categories: 
  - 10gen
  - MongoDC
  - customink
  - meetup
  - mongodb
  - mongomasters
  - mongosv
---
Shortly before [MongoSV 2011](http://blog.10gen.com/post/13885501875/announcing-the-mongodb-masters), 10gen announced the [MongoDB Masters](http://blog.10gen.com/post/13885501875/announcing-the-mongodb-masters) Program.

"The MongoDB Masters program is designed to recognize the achievements of leaders in the community and enable the exchange of knowledge between and among 10gen and the community."

I am honored to be counted among such a [great group of MongoDB enthusiasts](http://wiki.mongodb.org/display/DOCS/MongoDB+Masters). I was selected to join the Masters primarily because of my work with the [Washington DC MongoDB User Group](http://www.meetup.com/Washington-DC-MongoDB-Users-Group/) which I've been helping to organize for almost a year. The group has monthly meetings at [CustomInk](http://www.customink.com)'s headquarters in Tysons, VA.

The day before MongoSV, most of the MongoDB Masters met for the inaugural Masters Summit. The Masters Summit was run like an "un-conference"; the members decided on topics and broke into discussion groups to cover each topic. There were also a number of lightning talks.

We had break-out groups on 16 different topics including

* Operations, hosting, and production architecture
* Drivers
* MongoDB and Windows
* Reporting
<!--more-->
I participated in a couple of sessions about operations, one about hosting user groups, and one about reporting with MongoDB.

### MongoDB User Groups
I was able to share some of my experience with hosting the DC MongoDB User group in this session. There were a few other user group organizers who participated including: 

* [Harry Marr](http://twitter.com/harrymarr) and [David Mytton](http://twitter.com/davidmytton) from the London User Group
* [Mark Smalley](http://twitter.com/m_smalley) from the Malaysia User Group
* [Takahiro Inoue](http://twitter.com/doryokujin) from the Tokyo User Group

[Amelia](http://twitter.com/ameliamango), [Francesca](http://twitter.com/francescaPasha), [Meghan](http://twitter.com/meghanpgill), and [Sam](http://twitter.com/sam_10gen) who help organize community events for 10gen and [Chris Westin](http://twitter.com/cwestin63), also from 10gen, joined the discussion, too.

I was amazed to hear how large the Tokyo User Group is - over 600 members. They meet monthly on Saturdays, have multiple corporate sponsors, and great attendance at their meetings. I'm not sure how a Saturday user group meeting would go over in the US but suspect we'd see a very light turnout.

It was also great to hear some of the things that Chris Westin has done to organize the [Bay Area Large-Scale Production Engineering meetup](http://www.meetup.com/SF-Bay-Area-Large-Scale-Production-Engineering/). I read his blog post, [How to Run a Successful Tech Meetup](https://www.bookofbrilliantthings.com/blog/how-to-run-a-successful-tech-meetup), prior to the meeting so I had an idea about what some of his ideas were.  It was great to hear him echoing some of the things we've put into practice with the DC group.

After the discussion, I published a couple of blog posts on [ideas about how to run a successful user group meeting](http://nathenharvey.com/blog/2011/12/13/tips-for-hosting-a-tech-user-group/) and [some suggestions on the agenda / format for each meeting](http://nathenharvey.com/blog/2011/12/13/agenda-tips-for-a-tech-user-group/).

### Reporting with MongoDB
It seems there are still many questions around the best way to approach reporting on the data stored in a MongoDB. Sure, you can build custom reports easily enough with the data and that'll be even easier when the new aggregation framework is released. However, the real challenge comes when you need to expose data in MongoDB AND data housed in your RDBMS to the same reporting tools. This is certainly a challenge we face at CustomInk. I still don't feel that there is an easy answer in this area.  A couple of options were discussed including building custom ETL logic to load your MongoDB data into a RDBMS that can be used for reporting. I was particularly interested in the approach [Jonathan Wage](http://twitter.com/jwage) and his colleagues at [OpenSky](https://opensky.com/) are using. They've got a daemon that tails the MongoDB Oplog and updates a RDBMS as appropriate. This seems like a good approach and one I'd like to explore further.

### Side conversations
#### Configuration Management with Chef and Puppet
[Rick Copeland](http://twitter.com/rick446), [Mike Dirolf](http://twitter.com/mdirolf), [Mark Smalley](http://twitter.com/m_smalley), and I had a couple of conversations about Chef and Puppet. Of course the conversation included questions of which to use and why. At CustomInk, we've got experience with both so I shared some information on [Why We Chose Chef Over Puppet at CustomInk](http://nathenharvey.com/blog/2011/11/21/why-we-chose-chef-over-puppet-at-customink/).

#### Full-text search in MongoDB
During an open discussion, the question of full-text search within MongoDB came up. This topic seems to be a regular in any MongoDB roadmap discussions and the functionality always seems to be "very close, maybe in the n+1 release." I think it was [Mike Dirolf](http://twitter.com/mdirolf) who first voiced an opinion that I happen to share: "Stop working on it and focus on other features."

Search is no easy problem to solve and there are projects whose sole focus is on information indexing and retrieval. 10gen should stay focused on the core functionality of MongoDB and leave the search problems to Lucene, Solr, and other similar projects. I've used Solr with MongoDB successfully on one project and think this is the right way to go.

<img src="http://nathenharvey.s3-website-us-east-1.amazonaws.com/blog/images/mongodb_masters.jpg" width="320" height="250" alt="MongoDB Masters" />
I also agree with some of 10gen's concern that search is like a pandora's box. Once released, there will be a flood of feature requests and bug reports for this component which could quickly be distracting for the engineering team.

### Swag
It wouldn't be a 10gen event without a little swag, right?! MongoDB Masters were treated to custom coffee mugs, MongoDB Masters t-shirts, and great MongoDB Masters jackets.

## Next steps
The MongoDB Masters program is still pretty new. We're looking for ways to get the most out of the group. Google hangouts and IRC are where we're headed next but who knows where we'll go from there. I'd love to hear any ideas you have for how to make a group like this successful and productive.

If you want to keep-up with the MongoDB Masters on Twitter, you can follow the [Twitter list that I maintain](https://twitter.com/#!/nathenharvey/mongo-masters/members).

