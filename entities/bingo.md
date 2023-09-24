# Bingo

This project also integrates with the work of Brock Sexton's fork of WAN Show Bingo, for an interative experience whilst you watch the show live, and play it back at a later date.

We have teamed up to provide real-time notifications when a bingo square is confirmed right in our video player, allowing us to play back the bingo tiles, with second by second accuracy as you watch through newer VODs of the show (timestamped bingo tiles are available from the episode airing on September 29th/30th onwards)

current integration relies on bingo confirmations being placed into the Floatplane live chat, since we have reverse engineered it to allow us to send receive/send messages and scan content accordingly

regex:

```regexp
/"?(?:\w{1,}\s?){1,}"? Square confirmed ✅  https:\/\/wanshow\.bingo\//g
```
