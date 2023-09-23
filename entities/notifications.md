# Notifications

In app notifications are provided by RabbitMQ served via Web STOMP protocol, and are tied to a specific video ID

Here is an example in app notification payload:

```json
{
  "title":"Bingo Tile Confirmed", 
  "description":"Dan sighs heavily", 
  "avatar": {
    "src":"https://wanshow.bingo/resources/images/favicon-32x32.png"
    }, 
  "color":"green"
}
```

This example is for a WAN Show Bingo tile confirmation notification

# Floatplane Go Live Notifications
These notifications differ from the above example in many key ways, first, they are intern-only, not intended to be displayed to a user without some form of pre-processing.

The format is as follows:

## Stream Goes Live

When a stream goes live the following payload would be sent:

```json
{
   "id": "5c13f3c006f1be15e08e05c0",
   "isWAN": true,
   "title": "I'm Furious But NVIDIA Is Right - WAN Show September 22, 2023",
   "description": "<p>Unify and simplify your PC components! Check out Corsair’s iCUE Link Smart Ecosystem at <a href=\"https://lmg.gg/CorsairiCUELink\" rel=\"noopener noreferrer\"   target=\"_blank\">https://lmg.gg/CorsairiCUELink</a></p><p>Win a Hennessey Ford Bronco or $75K cash with no purchase necessary with the Ridge Wallet sweepstake! Check it out at <a   href=\"https://www.ridge.com/wan\" rel=\"noopener noreferrer\" target=\"_blank\">https://www.ridge.com/wan</a></p><p>Start your day on the right foot with AG1 at <a href=\"http://  drinkAG1.com/WANshow\" rel=\"noopener noreferrer\" target=\"_blank\">http://drinkAG1.com/WANshow</a></p><p><br></p><p>Podcast download: TBD</p>",
   "thumbnail": {
      "width": 1920,
      "height": 1080,
      "path": "https://pbs.floatplane.com/stream_thumbnails/5c13f3c006f1be15e08e05c0/429342495041409_1695430637206.jpeg",
      "childImages": [
         {
            "width": 400,
            "height": 225,
            "path": "https://pbs.floatplane.com/stream_thumbnails/5c13f3c006f1be15e08e05c0/429342495041409_1695430637206_400x225.jpeg"
         },
         {
            "width": 1200,
            "height": 675,
            "path": "https://pbs.floatplane.com/stream_thumbnails/5c13f3c006f1be15e08e05c0/429342495041409_1695430637206_1200x675.jpeg"
         }
      ]
   },
   "timestamp": 1695499906794
}
```

This is a real payload which was sent for the stream it represents, so the data is as accurate as it can get.

## Stream goes offline

When a floatplane stream goes offline, the following payload will be sent:

```json
{
  "offline": true,
  "timestamp": 1695499906795
}
```

There is no associated ID since Floaptlane only supports one stream at a time, therefore it is not needed
