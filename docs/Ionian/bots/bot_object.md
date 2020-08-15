# Bots

**Table of contents**

[TOC]

------------------------
Treated natively as`(DocSnapshot Object)`, but this information is not necessary to non-discordlist developers  

**Description:**  
Bot, document of 'bots' collection

> **NOTICE**:
> On requests, *only the properties under `public` are returned.* you do not need to specify `<fetch_res_data>.public.<properties>`when fetching info.
>
> It is only mentioned here for our own staff to understand.

## Properties

+ **public** _(object, required)_
  
  + **id** _(number, required)_ - Discord ID of the bot.
  + **name** _(string, required)_ - Name of the bot.
  + **uploaded_on** _(number, required)_ - Unix time, firestore serverTimeStamp.
  + **creator_id** _(number, required)_ - Discord ID of the uploader.
  + **creator_name** _(string | DocumentReference, required)_ - `@TODO either a pointer to users.<user>.name or have the name updated (with discrimnator)`
  + **icon_URL** _(string)_ - Optional URL to the bot icon desired.
  + **tags** _(array_(string)_, required?)_ - Tags attached to the bot.
+ **description** _(string, required)_ - A description describing the bot.`
  
  + **status** _(object)_
    + **approvalStatus** _(enum)_
      + **pending** _(string)_ - Default for users.
      + **approved** _(string)_ - `Note: Mods and Staff get approved automatically.`
      + **rejected** _(string)_ - Moderators have looked through it and rejected it.
  + **queue** _(number)_ - Number in the queue to be approved by mods. (-1 means is has already been reviewed)
  
+ **stats** _(object)_ - Non-public object containing API Bot stats

  + Info - To view more info please visit [Bot Stats](./bot_stats.md)

  > *@TODO* Explain

**EXAMPLE: **

```json
// Stored (Below)

{
    "public": {
        // root object of response.
        "id": "1234567890",
        "name": "My first bot",
        "uploaded_on": "1597373179",
        "creator_id": "908765421",
        "creator_name": "Wumpus#6969",
        "icon_URL": "https://static.discordlist.gg/public/assets/profiles/908765421/1597372331.jpeg",
        "tags": ["Utilities", "Pokemon"],
        "description": "Hey guys i [i]cough[/i] really like this song.",
        "status": {
            "approvalStatus": "approved",
            "queue": "-1"
        },
        "stats": {
            // Cannot be grabbed outside of stats endpoints. Not visible.
            // ...
        }
    }
}


```

Again, for unelevated users, only the following can be seen: 

> (Elevated users currently cannot see the rest either, however this is being worked on.)

```json
// I feel like I need to make this super clear again.
// Returns (Below)

{
    "id": "1234567890",
	"name": "My first bot",
    // ... and so on. note the lack of public object.
}
```



`json**, xml` - json is preferred

> In fact, I haven't implemented returning XML yet lol

## API Requests
This is placeholder text for the description that should go here.

### Paginate Bots

| Endpoint         | Method | Supports Queries | Auth. Required |
| ---------------- | :----: | :--------------: | -------------- |
| /api/bots/search |  GET   |       Yes        | None           |

 __query__:

- `query` - the search term

- `page` - specifies the required  

- `limit`

- > `@TODO Finish and also provide examples`

## TBA

...
