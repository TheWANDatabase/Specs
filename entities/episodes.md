# Entities#Episodes

Current Layout:

|     Field     |   Type    |        Nullable        | Description                                                                                                              |
|:-------------:|:---------:|:----------------------:|:-------------------------------------------------------------------------------------------------------------------------|
|      id       |   Text    | <ul><li>[ ] </li></ul> | The ID of the episode in question, this is the unique portion of the episode's Youtube Watch URL                         |
|    youtube    |   Text    | <ul><li>[ ] </li></ul> | The url of the Youtube VOD[^1]                                                                                           |
|  floatplane   |   Text    | <ul><li>[x] </li></ul> | The url of the Floatplane VOD (if it exists)[^2]                                                                         |
|     title     |   Text    | <ul><li>[x] </li></ul> | The title of the episode as seen on Youtube without the date (since that is stored elsewhere)                            |
|     aired     |   Date    | <ul><li>[ ] </li></ul> | The date the episode was originally aired[^3]                                                                            |
|  description  |   Text    | <ul><li>[x] </li></ul> | The description of the video as seen on Youtube                                                                          |
|     cast      |   Int[]   | <ul><li>[ ] </li></ul> | An array of integers which mapped to the IDs of entries in the cast table                                                |
|   duration    |    Int    | <ul><li>[ ] </li></ul> | The number of seconds that the show goes on for                                                                          |
| duration_text |   Text    | <ul><li>[ ] </li></ul> | Human readable duration based of the field above / Or "live" if show is ongoing[^1]                                      |
|     flags     |  Object   | <ul><li>[ ] </li></ul> | Encoded flags listed against an episode, this is decoded to boolean values using [masks available below](#episode-flags) |
|   stream_id   |   Text    | <ul><li>[x] </li></ul> | The video ID on CloudFlare's Stream platform (if present)[^4]                                                            |
| last_modified | Timestamp | <ul><li>[ ] </li></ul> | An ISO8601 timestamp representing the last time a change was made to the entity                                          |

### References

[^1]: This field will be getting removed entirely because it is wasteful

[^2]: This field will be converted from a URL to a unique ID and reconstructed on the
client side

[^3]: This field may on occasion be out of sync by about 24 hours due to the delays
in VOD availability

[^4]: This field is only populated for videos which have a possible "known good" copy
and are otherwise corrupted

---

# Episode Flags

The episode flag table is currently being rebuilt based off of the update database schema, and will be updated here
when it is complete.