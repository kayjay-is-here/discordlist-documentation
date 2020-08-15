# Bot Stats

> This is a property of the [bot](./bot_object.md) object.
Analytical statistics in raw data on bot activities

**Table of Contents**

[TOC]

> @TODO Make sure the behavior of the API actually does as the documentation says it should

## About

Bot statistics are stored as arrays of _stat_ objects.

> In development, the `Bot` object contains a `stats` property which contains a pointer to our `\stats` database

The following table contains the columns `Updatable` and `Settable`. 

​	If a property is `updatable`, you may provide it in `PUT`requests, which will __aggregate__ the data submitted to already existing data

​	If a property is `settable`, you may provide it in `POST`requests, which will __override__ existing data with the data submitted.

If a property has neither, then it is immutable and is set at creation/automatically generated

> Okay, this isn't done on the code yet, so I probably should work on that first before writing this documentation. Oh well~ 
>
> -kjl3080

Each element contains a object with the following properties:

| property     | type   | description                                                  | required? | Updatable? | Settable? |
| ------------ | ------ | ------------------------------------------------------------ | --------- | ---------- | --------- |
| `id`         | number | The ID of the bot  *Must always be provided*.                | Yes       | No         | No        |
| `creator_id` | number | The ID of the author. *Must always be provided.*             | Yes       | No         | No        |
| `timestamp`  | N/A    | Firebase Timestamp of when this array was pushed.            | No        | No         | No        |
| `servers`    | number | The amount of servers this bot is in.                        | No        | Yes        | Yes       |
| `users`      | number | The total amount of users aggregated in all servers this bot is connected to | No        | No         | Yes       |
| `commands`   | number | Total amount of commands ran since it's submission on this site | No        | Yes        | No        |
| `voice`      | number | Time in minutes the bot is in voice chat                     | No        | Yes        | No        |
| `other`      | object | **Do not use this, this is to provide backwards compatibility in future updates* | No        | No         | No        |

> **Developers Note:** ~~There are multiple things we might want to do. Should we handle the aggregation of users and stuff ourselves? 
> Yes, I think we should. Well, `@TODO`then. Another thing is should we include the new amount of each command ran? For "most used commands and stuff?"~~ 
>
> > we should worry about it in v2.
>
> Actually, should we just have POST requests not set, but rather increment the counts?
>
> > Yeah, okay, sure. uh, we gotta update this section.



The following is a stat object.

**Example:**

```JSON
{	
    "id":"1234567890", // immutable, IDENTITY_KEY
    "creator_id":"9087654321", // immutable
  	"timestamp": "183478913", // immutable
    "users":"420",
    "commands":"2003",
    "voice":"133",
    "other": {
   		// Left here for combatability reasons
    	
    	/*
    	"top_commands":[{
    		"command":"help",
    		"count":"232"
		},
	 	{
         // ...
     	}]
     	*/
	}
}
```





## Endpoint

`/api/bots/:id/stats`
Param `id`: Discord bot's ID.

Currently, we only support the following REST requests:
`GET` - Fetch stored information on bot stats. See [Get Bot Stats](#get-bot-stats)
`POST` - Send information to set the bot stats. See [Update Bot Stats](#update-bot-stats)

## Requests

### Headers

All RESTful requests to /api/bot/:id/stats require the following Header:

- **discord_id** _(string)_ - the discord ID of the author of the bot.

- **api_key** _(string)_ - Unhashed API Key that belongs to the owner.

  > NOTE: Make sure the api_key is in lowercase!

- **(scopes)** _(string | array(string))_ - *Optional* The API scopes authorized. Defaults to `['stats']`.

- If any of the information is invalid, a `400`, `401` or `403` error will be returned.

> For more information on API Keys, read [API Keys](../auth/api_keys.md).

__Example:__
Format: `JSON`

```json
{
    "discord_id":"123456789",
    "api_key":"0dd2aff4-6432-4f30-b3f0-6ecccf0c9192",
    "scopes": ["basic","stats"]
}
```

> TODO more **thoroughly** explain how this works in API KEYS

### Response

The response will be returned in `JSON` Format.



## Available Actions



### Get bot Stats

Fetches the current bot stats as timestamped array entries. `:id` is the discord ID of the bot.

Returns an array which contains stat object elements. In addition, `id`,`creator_id`, and `last_updated` are returned as well.

| Endpoint              | Method |         Auth Required          | Path queries? |
| --------------------- | :----: | :----------------------------: | :-----------: |
| `/api/bots/:id/stats` | *GET*  | `API_KEY`, scopes: `['stats']` |      Yes      |

Queries: 

+ `ascending`(Boolean, optional) - If the oldest entries should be last. Defaults to `false`.

+ `limit`(*number*, optional) - How many entries to return. Always counts from the latest entry. Defaults to 200 entries. if the limit is 0, all entries are returned.

  > Is this confusing? I'll change it later



**Example**:

The following request

```http
GET https://discordlist.gg/api/bots/123456790/stats?limit=50&ascending=false
```

Assuming proper headers would return

```json
{
    // Identifying information
    "id":"1234567890",
    "creator_id":"9087654321",
    "last_updated":"183478913"
    // the stats array
    "stats": [
        {	
    		"id":"55", // immutable, IDENTITY_KEY
    		 // immutable
  			"timestamp": "183478913" // immutable
    		// ... 
		}, 
        {
            "id":"213412512",
           	"creator_id":"9087654321",
            "timestamp":"183475313" // Notice how the time is earlier. This is because of our "ascending" setting.
            // ...
        }
		// ...
	]
}
```



## Set bot Stats

Description goes here

| Endpoint              | Method | Auth Required                  | Path queries? |
| --------------------- | :----: | ------------------------------ | ------------- |
| `/api/bots/:id/stats` | *POST* | `API_KEY`, scopes: `['stats']` | No            |

The following request must contain the following `body`



explanation goes here

example goes here 

## Update bot Stats

Description goes here

| Endpoint              | Method | Auth Required                  | Path queries? |
| --------------------- | :----: | ------------------------------ | ------------- |
| `/api/bots/:id/stats` |  PUT   | `API_KEY`, scopes: `['stats']` | No            |

Explanation goes here