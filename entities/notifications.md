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