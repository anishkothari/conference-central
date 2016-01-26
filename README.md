# Conference Central
Project 4 of the Udacity Fullstack Nanodegree. This application runs on Google App Engine.

Features include the ability to create conferences, sessions, view conferences and sessions. Users can register/unregister for conferences, add/remove sessions to their wishlists after logging in with their Google credentials. Using the Task Queue, e-mails are sent to the conference organizer after they have created a conference. Using Memcache, announcements are made when there are limited seats remaining in a conference and if there a speaker presenting more than one session, they will be set as the featured speaker for the conference.

The following property types are used for sessions:
```
name = ndb.StringProperty(required=True)
highlights = ndb.StringProperty
speaker = ndb.StringProperty()
duration = ndb.IntegerProperty()
typeOfSession = ndb.StringProperty()
date = ndb.DateProperty()
startTime = ndb.TimeProperty()
```

Design choices for session and speaker functionality include the appropriate property types to be stored in NDB. Name, highlights, speaker and session type are all stored as string properties while duration in minutes is stored as an integer property, date is stored as a date property and session start time is stored as a time property.

Sessions are implemented similar to conferences, although queries are implemented somewhat differently. For the ease of testing (and lack of a front-end), queries are independent of each other.
Speaker functionality is implemented by saving the appropriate speakers in Memcache and retrieving it when displaying the conference details.

Additional queries implemented find sessions by a speaker's name (getSessionsByName) and by session highlights (getSessionsByHighlights). The purpose of the highlights query is to find similar sessions so user's can add them to their wishlists easily.

How would you handle a query for all non-workshop sessions before 7 pm? What is the problem for implementing this query? What ways to solve it did you think of?

The problem implementing this query is that multiple inequalities can't be queried in datastore on more than one field (typeOfSession and startTime in this case). I would implement this using two queries - one to find non-workshop sessions and another query for sessions before 7pm. The query to find non-workshop sessions should use an equality filter and the time query could use an inequality filter.

## Products
- [App Engine][1]

## Language
- [Python][2]

## APIs
- [Google Cloud Endpoints][3]

## Setup Instructions
1. Update the value of `application` in `app.yaml` to the app ID you
   have registered in the App Engine admin console and would like to use to host
   your instance of this sample.
1. Update the values at the top of `settings.py` to
   reflect the respective client IDs you have registered in the
   [Developer Console][4].
1. Update the value of CLIENT_ID in `static/js/app.js` to the Web client ID
1. (Optional) Mark the configuration files as unchanged as follows:
   `$ git update-index --assume-unchanged app.yaml settings.py static/js/app.js`
1. Run the app with the devserver using `dev_appserver.py DIR`, and ensure it's running by visiting your local server's address (by default [localhost:8080][5].)
1. (Optional) Generate your client library(ies) with [the endpoints tool][6].
1. Deploy your application.


[1]: https://developers.google.com/appengine
[2]: http://python.org
[3]: https://developers.google.com/appengine/docs/python/endpoints/
[4]: https://console.developers.google.com/
[5]: https://localhost:8080/
[6]: https://developers.google.com/appengine/docs/python/endpoints/endpoints_tool
