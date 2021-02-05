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
   * [getMotionActivityRoster](#getMotionActivityRoster)
   * [getMotionTeamRoster](#getMotionTeamRoster)
   * [getMotionActivitySummary](#getMotionActivitySummary)

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

### getMotionActivityRoster

For a given event, retrieve a list of motion activity for top participants and teams.

#### Parameters
* `event_id` (required unless requesting a program roster) The ID of the event from which you wish to retrieve participants
* `roster_type` (required) Possible values include participant, team, program
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
`https://load.boundlessfundraising.com/mobiles/democdsb/getMotionActivityRoster?event_id=1234&team_id=5678&roster_type=team&list_size=5`

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

#### Sample Program Roster Call to Staging
`https://load.boundlessfundraising.com/mobiles/democdsb/getMotionActivityRoster?roster_type=program&list_size=5`

#### Sample Program Roster Response
``` JSON
{
    "metric": "steps",
    "activities": {
        "topParticipants": [
            {
                "rank": 1,
                "total": "17770298",
                "name": "Joyce B.",
                "id": "2891927",
                "event_id": "3881"
            },
            {
                "rank": 2,
                "total": "6851755",
                "name": "Jessica S.",
                "id": "399471829",
                "event_id": "1100"
            },
            {
                "rank": 3,
                "total": "3541131",
                "name": "Niasha H.",
                "id": "2881900",
                "event_id": "9398"
            },
            {
                "rank": 4,
                "total": "1738421",
                "name": "Kenneth B.",
                "id": "9992772",
                "event_id": "1992"
            },
            {
                "rank": 5,
                "total": "1681865",
                "name": "Joe B.",
                "id": "2881992",
                "event_id": "8477"
            }
        ],
        "topTeams": [
            {
                "rank": 1,
                "total": "19336535",
                "name": "The Not Alone Rangers",
                "id": "288819",
                "event_id": "2992"
            },
            {
                "rank": 2,
                "total": "17770298",
                "name": "Stewart Family Autos",
                "id": "581061",
                "event_id": "1122"
            },
            {
                "rank": 3,
                "total": "14852366",
                "name": "St. Francis Hospital",
                "id": "299910",
                "event_id": "2983"
            },
            {
                "rank": 4,
                "total": "12053693",
                "name": "Alpha Beta",
                "id": "199271",
                "event_id": "1112"
            },
            {
                "rank": 5,
                "total": "12015957",
                "name": "Main Street Bankers",
                "id": "229933",
                "event_id": "2221"
            }    
        ]
    }
}
```

### getMotionTeamRoster

For a given team, retrieve a list of motion activity for participants of that team.

#### Parameters
* `event_id` (required) The ID of the event from which you wish to retrieve participants
* `team_id` (required) The ID of the team you wish to retrieve

#### Sample Team Roster Call to Staging
`https://load.boundlessfundraising.com/mobiles/democdsb/getMotionTeamRoster?event_id=1234&roster_type=team&list_size=5`

#### Sample Teams Roster Response

``` JSON
{
   "metric":"steps",
   "team_member_list":[
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


#### Sample Call to Staging for a Program
`https://load.boundlessfundraising.com/mobiles/{boundlessDB}/getMotionActivitySummary?activity_scope=program`

#### Sample Response for a Program
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

#### Sample Call to Staging for a Team
`https://load.boundlessfundraising.com/mobiles/{boundlessDB}/getMotionActivitySummary?activity_scope=team&event_id=1234&team_id=56789`

#### Sample Response for a Team

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
