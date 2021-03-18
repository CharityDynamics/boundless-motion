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
   "metric":"distance",
   "activities":[
        {
            "rank": 1,
            "total": 15196.3,
            "name": "Oliver J.",
            "id": "1001841",
            "event_id": "1061",
            "duration": "3288"
        },
        {
            "rank": 2,
            "total": 128.76,
            "name": "Ben T.",
            "id": "1001962",
            "event_id": "1061",
            "duration": "0"
        },
        {
            "rank": 3,
            "total": 105.49,
            "name": "Ben T.",
            "id": "1001963",
            "event_id": "1061",
            "duration": "0"
        },
        {
            "rank": 4,
            "total": 57.21,
            "name": "David P.",
            "id": "1002163",
            "event_id": "1061",
            "duration": "684"
        },
        {
            "rank": 5,
            "total": 41.49,
            "name": "Byrony Z.",
            "id": "1001685",
            "event_id": "1061",
            "duration": "1452"
        }
   ]
}
```

#### Sample Teams Roster Call to Staging
`https://load.boundlessfundraising.com/mobiles/{boundlessDB}/getMotionActivityRoster?event_id=1234&roster_type=team&list_size=5`

#### Sample Teams Roster Response

``` JSON
{
    "metric": "distance",
    "team_member_list": [
        {
            "duration": "3288",
            "user_id": "1001841",
            "total": 15196.3,
            "first_name": "Oliver",
            "last_name": "James"
        },
        {
            "duration": "0",
            "user_id": "1001843",
            "total": 6.41,
            "first_name": "Liam",
            "last_name": "Potter"
        },
        {
            "duration": "0",
            "user_id": "1001911",
            "total": 0,
            "first_name": "Diego",
            "last_name": "Muoz"
        },
        {
            "duration": "0",
            "user_id": "1001844",
            "total": 0,
            "first_name": "Ethan",
            "last_name": "Lilly"
        },
        {
            "duration": "0",
            "user_id": "1001908",
            "total": 0,
            "first_name": "Oliva",
            "last_name": "Pope"
        },
        {
            "duration": "0",
            "user_id": "1001842",
            "total": 0,
            "first_name": "Sansa",
            "last_name": "James"
        },
        {
            "duration": "0",
            "user_id": "1001910",
            "total": 0,
            "first_name": "Thomas",
            "last_name": "Fitzgerald"
        }
    ]
}
```

#### Sample Program Roster Call to Staging
`https://load.boundlessfundraising.com/mobiles/{boundlessDB}/getMotionActivityRoster?roster_type=program&list_size=5`

#### Sample Program Roster Response
``` JSON
{
    "metric": "miles",
    "activities": {
        "topParticipants": [
            {
                "rank": 1,
                "total": 15196.3,
                "name": "Oliver J.",
                "id": "1001841",
                "event_id": "1061",
                "duration": "3288"
            },
            {
                "rank": 2,
                "total": 128.76,
                "name": "Ben T.",
                "id": "1001962",
                "event_id": "1061",
                "duration": "0"
            },
            {
                "rank": 3,
                "total": 105.49,
                "name": "Ben T.",
                "id": "1001963",
                "event_id": "1061",
                "duration": "0"
            },
            {
                "rank": 4,
                "total": 57.21,
                "name": "David P.",
                "id": "1002163",
                "event_id": "1061",
                "duration": "684"
            },
            {
                "rank": 5,
                "total": 41.49,
                "name": "Byrony Z.",
                "id": "1001685",
                "event_id": "1061",
                "duration": "1452"
            }
        ],
        "topTeams": [
            {
                "rank": 1,
                "total": 15202.7,
                "name": "Boundless",
                "id": "1040",
                "event_id": "1061",
                "duration": "3288"
            },
            {
                "rank": 2,
                "total": 113.23,
                "name": "Bens Test Team",
                "id": "1080",
                "event_id": "1061",
                "duration": "0"
            },
            {
                "rank": 3,
                "total": 57.21,
                "name": "Awesome Sauce 2",
                "id": "1121",
                "event_id": "1061",
                "duration": "684"
            },
            {
                "rank": 4,
                "total": 50,
                "name": "Charity Dynamics UX",
                "id": "1050",
                "event_id": "1061",
                "duration": "0"
            },
            {
                "rank": 5,
                "total": 41.49,
                "name": "Team Work 2",
                "id": "1021",
                "event_id": "1061",
                "duration": "1452"
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
`https://load.boundlessfundraising.com/mobiles/{boundlessDB}/getMotionTeamRoster?event_id=1234&roster_type=team&list_size=5`

#### Sample Teams Roster Response

``` JSON
{
    "metric": "distance",
    "team_member_list": [
        {
            "duration": "3288",
            "user_id": "1001841",
            "total": 15196.3,
            "first_name": "Oliver",
            "last_name": "James"
        },
        {
            "duration": "0",
            "user_id": "1001843",
            "total": 6.41,
            "first_name": "Liam",
            "last_name": "Potter"
        },
        {
            "duration": "0",
            "user_id": "1001911",
            "total": 0,
            "first_name": "Diego",
            "last_name": "Muoz"
        },
        {
            "duration": "0",
            "user_id": "1001844",
            "total": 0,
            "first_name": "Ethan",
            "last_name": "Lilly"
        },
        {
            "duration": "0",
            "user_id": "1001908",
            "total": 0,
            "first_name": "Oliva",
            "last_name": "Pope"
        },
        {
            "duration": "0",
            "user_id": "1001842",
            "total": 0,
            "first_name": "Sansa",
            "last_name": "James"
        },
        {
            "duration": "0",
            "user_id": "1001910",
            "total": 0,
            "first_name": "Thomas",
            "last_name": "Fitzgerald"
        }
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
    "duration": "7877",
    "metric": "distance",
    "total": "15654.75",
    "total_participants": "49"
}
```

#### Sample Call to Staging for a Team
`https://load.boundlessfundraising.com/mobiles/{boundlessDB}/getMotionActivitySummary?activity_scope=team&event_id=1234&team_id=56789`

#### Sample Response for a Team

``` JSON
{
    "duration": "3",
    "metric": "distance",
    "total": "0.35",
    "goal": "1000"
}
```

#### Sample Call to Staging for a Participant
`https://load.boundlessfundraising.com/mobiles/{boundlessDB}/getMotionActivitySummary?activity_scope=user&event_id=1234&user_id=987654`


#### Sample Response for a Participant

``` JSON
{
    "duration": "1452",
    "metric": "distance",
    "total": "41.48",
    "goal": "50",
    "name": "Byrony Zeigler"
}
```
