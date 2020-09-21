# Boundless Motion REST API

## Overview

Boundless Motion allows fundraisers to engage in and track their physical activity while they raise money for their favorite cause. Depending on their event registration, users can track their run, walk, ride or other activity leading up to and including event day. 

The Boundless Motion API allows activity data to be displayed outside of the Boundless Fundraising mobile app. Using this API, developers can display details and summaries of a participant, team, event and program actiivty on third party websites.

## Table of Contents

* [Support](#Support)
* [Request URLs](#Request-URLs)
   * [Staging](#Staging-URLs)
   * [Production](#Production-URLs)
* [Authentication](#Authentication)
* [Methods](#Methods)
   * [getMotionParticipants](#getMotionParticipants)
   * [getMotionActivityRoster](#getMotionActivityRoster)
   * [getMotionTeamRoster](#getMotionTeamRoster)
   * [getMotionActivitySummary](#getMotionActivitySummary)
   * [getMotionParticipantActivities](#getMotionParticipantActivities)
   * [addMotionActivity](#addMotionActivity)

## Support
For API support, please email support@boundlessfundraising.com.

## Request URLs
Boundless Motion APIs can be made to both staging and production environments. The request URL must include the boundless database name along with the API method being called:

### Staging URL:
`https://load.boundlessfundraising.com/mobiles/{boundlessDB}/{motionApiMethod}`

### Production URL:
`https://loadprod.boundlessfundraising.com/mobiles/{boundlessDB}/{motionApiMethod}`

## Authentication
Access to the Boundless Motion API is granted by providing your username and password using HTTP basic authentication.  If you have a Boundless Motion contract, you can request a username and password by emailing support@boundlessfundraising.com. All Motion API calls require this authentication to be sent.

## Methods

### getMotionParticipants
For a given event, retrieve a list of user IDs for participants who have connected to Boundless Motion.

#### Parameters
* `event_id` (required) The ID of the event from which you wish to retrieve participants
* `from` (required) Starting date for the results you wish to retrieve, format `YYYY-MM-DD`
* `to` (required) Ending date for the results you wish to retrieve, format `YYYY-MM-DD`

#### Sample Call to Staging
`https://load.boundlessfundraising.com/mobiles/{boundlessDB}/getMotionParticipants?event_id=1234&from=2020-04-30&to=2020-07-27`

#### Sample Response

``` JSON
{
   "participants":[
      "1001941",
      "1001901",
      "1001846",
      "1001906",
      "1001842",
      "1001910",
      "1001843",
      "1001903",
      "1001841",
      "1001908",
      "1001913",
      "1001685",
      "1001902"
   ]
}
```

### getMotionActivityRoster

For a given event, retrieve a list of motion activity for top participants and teams.

#### Parameters
* `event_id` (required) The ID of the event from which you wish to retrieve participants
* `roster_type` (required) Possible values include participant or team
* `list_size` (required) How many results you wish to retrieve 

#### Sample Participant Roster Call to Staging
`https://load.boundlessfundraising.com/mobiles/{boundlessDB}/getMotionActivityRoster?event_id=1234&roster_type=participant&list_size=5`

#### Sample Participant Roster Response

``` JSON
{
   "metric":"steps",
   "activities":[
      {
         "rank":1,
         "total":"95000",
         "name":"Karl M.",
         "id":"2120"
      },
      {
         "rank":2,
         "total":"90000",
         "name":"Rachel A.",
         "id":"1005402"
      },
      {
         "rank":3,
         "total":"55000",
         "name":"Abraham L.",
         "id":"1014422"
      },
      {
         "rank":4,
         "total":"35000",
         "name":"Jon F.",
         "id":"1014423"
      },
      {
         "rank":5,
         "total":"15000",
         "name":"Sarah T.",
         "id":"1014322"
      }
   ]
}
```

#### Sample Teams Roster Call to Staging
`https://load.boundlessfundraising.com/mobiles/demokhs/getMotionActivityRoster?event_id=1234&roster_type=team&list_size=5`

#### Sample Teams Roster Response

``` JSON
{
   "metric":"steps",
   "activities":[
      {
         "rank":1,
         "total":"365422",
         "name":"Leah's Friends",
         "id":"1470"
      },
      {
         "rank":2,
         "total":"301111",
         "name":"Team Work",
         "id":"1410"
      },
      {
         "rank":3,
         "total":"101111",
         "name":"Johnna Team",
         "id":"1330"
      },
      {
         "rank":4,
         "total":"99213",
         "name":"Franks Team",
         "id":"1500"
      },
      {
         "rank":5,
         "total":"99213",
         "name":"Step It Up",
         "id":"1500"
      }
   ]
}
```
<!-- 
#### Sample Companies Roster Call to Staging
`https://load.boundlessfundraising.com/mobiles/demokhs/getMotionActivityRoster?event_id=1234&roster_type=company&list_size=5`

#### Sample Companies Roster Response

``` JSON
{
   "metric":"steps",
   "activities":[
      {
         "rank":1,
         "total":"39920",
         "name":"Acme, Inc.",
         "id":"1430"
      },
      {
         "rank":2,
         "total":"299110",
         "name":"Amalgamated Industries",
         "id":"1992"
      },
      {
         "rank":3,
         "total":"190029",
         "name":"Sprockets USA",
         "id":"1140"
      },
      {
         "rank":4,
         "total":"29923",
         "name":"Innotech",
         "id":"1002"
      },
      {
         "rank":5,
         "total":"1089",
         "name":"Burger World",
         "id":"1010"
      }
   ]
}
``` -->


### getMotionTeamRoster

For a given team, retrieve a list of motion activity for participants of that team.

#### Parameters
* `event_id` (required) The ID of the event from which you wish to retrieve participants
* `team_id` (required) The ID of the team you wish to retrieve

#### Sample Team Roster Call to Staging
`https://load.boundlessfundraising.com/mobiles/demokhs/getMotionTeamRoster?event_id=1234&roster_type=team&list_size=5`

#### Sample Teams Roster Response

``` JSON
{
   "metric":"steps",
   "activities":[
      {
         "user_id": "301111",
         "total": 30402,
         "first_name": "John",
         "last_name": "Henry"
      },
      {
         "user_id": "399201",
         "total": 20911,
         "first_name": "Barbara",
         "last_name": "Jones"
      },
   ]
}
```

### getMotionActivitySummary
New call named getMotionActivitySummary is available with the same authentication, params, etc. as the previous call. The following is a sample call:

For a given event, retrieve a list of motion activity for top participants and teams.

#### Parameters
* `activity_scope` (required) Possible values include user, team, event and program
* `event_id` (required) The ID of the event for which you wish to retrieve activity summary data
* `team_id` (required) The ID of the team for which you wish to retrieve activity summary data
* `user_id` (required) The ID of the participant for which you wish to retrieve activity summary data
<!-- * `company_id` (required) The ID of the company for which you wish to retrieve activity summary data -->


#### Sample Call to Staging for an Program
`https://load.boundlessfundraising.com/mobiles/{boundlessDB}/getMotionActivitySummary?activity_scope=program`

#### Sample Response for an Program
Note: Program-level activity summary is updated hourly.

``` JSON
{
   "goal": "5000",
   "metric": "distance",
   "total": "39760.16"
}
```

#### Sample Call to Staging for an Event
`https://load.boundlessfundraising.com/mobiles/{boundlessDB}/getMotionActivitySummary?activity_scope=event&event_id=1234`

#### Sample Response for an Event
Note: Motion does not store an activity goal for events, so only total achieved activity for the event is returned.

``` JSON
{
   "metric":"steps",
   "total":"141957",
   "total_participants":"11"
}
```
<!-- 
#### Sample Call to Staging for a Company
`https://load.boundlessfundraising.com/mobiles/{boundlessDB}/getMotionActivitySummary?activity_scope=company&event_id=1234&company_id=56789`

#### Sample Response for an Company

``` JSON
{
  "metric": "steps",
  "total": "29910"
}
``` -->

#### Sample Call to Staging for a Team
`https://load.boundlessfundraising.com/mobiles/{boundlessDB}/getMotionActivitySummary?activity_scope=team&event_id=1234&team_id=56789`

#### Sample Response for an Team

``` JSON
{
  "metric": "steps",
  "total": "51756",
  "goal": "60000"
}
```

#### Sample Call to Staging for a Participant
`https://load.boundlessfundraising.com/mobiles/{boundlessDB}/getMotionActivitySummary?activity_scope=user&event_id=1234&user_id=987654`


#### Sample Response for a Participant

``` JSON
{
  "metric": "steps",
  "total": "14916",
  "goal": "15000",
  "name": "Howard Jones"
}
```


### getMotionParticipantActivities
New call named getMotionActivitySummary is available with the same authentication, params, etc. as the previous call. The following is a sample call:

For a given event, retrieve a list of motion activity for top participants and teams.

#### Parameters
* `event_id` (required) The ID of the event for which you wish to retrieve activity data
* `user_id` (required) The ID of the participant for which you wish to retrieve activity data
* `from` (required) Starting date for the results you wish to retrieve, format `YYYY-MM-DD`
* `to` (required) Ending date for the results you wish to retrieve, format `YYYY-MM-DD`

#### Sample Call to Staging
`https://load.boundlessfundraising.com/mobiles/{boundlessDB}/getMotionParticipantActivities?event_id=1234&user_id=987654&from=2020-04-30&to=2020-07-27`


#### Sample Response

``` JSON
{
   "type":"run",
   "metric":"steps",
   "activity":[
      {
         "id":"739",
         "date":"2020-06-26",
         "total":"5",
         "duration":"02:10"
      },
      {
         "id":"724",
         "date":"2020-06-26",
         "total":"54",
         "duration":"18:07"
      },
      {
         "id":"736",
         "date":"2020-06-24",
         "total":"500",
         "duration":"03:03"
      }
   ]
}
```

### addMotionActivity
The following is a sample request URL for adding an activity for a participant.

#### Parameters
* `user_id` (required) Possible values include participant, team, and event 
* `event_id` (required) The ID of the event for which you wish to retrieve activity summary data
* `date` (required) The date of the activity `YYYY-MM-DD`
* `amount` (required) The amount of the activity achieved
* `duration` (required) The duration of the activity `HH:MM`

#### Sample Call to Staging
`https://load.boundlessfundraising.com/mobiles/{boundlessDB}/addMotionActivity?user_id=987654&event_id={eventId}&date=2020-06-26&amount=5&duration=2:10`

#### Sample Response

``` JSON
{
   status: "success",
   success: 1
}
```
