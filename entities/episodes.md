# Entities#Episodes

Current Layout:

|     Field     |   Type    |        Nullable        | Description                                                                                                              |
| :-----------: | :-------: | :--------------------: | :----------------------------------------------------------------------------------------------------------------------- |
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

[^1]: This field will begetting removed entirely because it is wasteful

[^2]: This field will beconverted from a URL to a unique ID and reconstructed on the
client side

[^3]: This field may onoccasion be out of sync by about 24 hours due to to the delays
in VODavailability

[^4]: This field is onlypopulated for videos which have a possible "known good" copy
and are otherwisecorrupted

---

# Episode Flags

| Flag    | Description                                                                                                                |
| :------ | :------------------------------------------------------------------------------------------------------------------------- |
| thumb   | Video has a thumbnail hosted on our CDN                                                                                    |
| aod     | Video has an AOD / Audio On Demand File (Hosted on our CDN)                                                                |
| vod     | Video has an VOD / Video On Demand File (Hosted on our CDN)                                                                |
| vtt     | Video has a transcript file available                                                                                      |
| private | Video is private - These videos are not recognized by the API                                                              |
| stream  | Video is available via Stream Player[^4][^5]                                                                               |
| live    | Video is currently being actively livestreamed by LMG (This flag should be exclusive!)                                     |
| corrupt | Video is corrupted and users should be warned of this when viewing VOD content.                                            |
| cw      | Video has a content warning applied, this is usually because it is an older video before they were so careful about things |
| guest   | Video features one or more guests to the show (non LMG staff)                                                              |
| event   | This show was streamed from an LTX or other industry event                                                                 |
| mm      | Video features the use of Merch Messages                                                                                   |
| pl      | Video features the launch of a product by LMG/Creator Warehouse                                                            |

### References

[^5]: [See Cloudflare docs](https://developers.cloudflare.com/stream/)