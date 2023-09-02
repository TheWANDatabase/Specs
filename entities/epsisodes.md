# Entities#Episodes

Current Layout:

|     Field     |   Type    |        Required        | Description                                                                                                                                       |
| :-----------: | :-------: | :--------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------ |
|      id       |   Text    | <ul><li>[x] </li></ul> | The ID of the episode in question, this is the unique portion of the episode's Youtube Watch URL                                                  |
|    youtube    |   Text    | <ul><li>[x] </li></ul> | The url of the Youtube VOD <sup><a href="#episodes-origin-1" /> [[1]](#episodes-ref-1)</sup>                                                      |
|  floatplane   |   Text    | <ul><li>[ ] </li></ul> | The url of the Floatplane VOD (if it exists) <sup><a href="#episodes-origin-2" /> [[2]](#episodes-ref-2)</sup>                                    |
|     title     |   Text    | <ul><li>[ ] </li></ul> | The title of the episode as seen on Youtube without the date (since that is stored elsewhere)                                                     |
|     aired     |   Date    | <ul><li>[x] </li></ul> | The date the episode was originally aired <sup><a href="#episodes-origin-3" /> [[3]](#episodes-ref-3)</sup>                                       |
|  description  |   Text    | <ul><li>[ ] </li></ul> | The description of the video as seen on Youtube                                                                                                   |
|     cast      |   Int[]   | <ul><li>[x] </li></ul> | An array of integers which mapped to the IDs of entries in the cast table                                                                         |
|   duration    |    Int    | <ul><li>[x] </li></ul> | The number of seconds that the show goes on for                                                                                                   |
| duration_text |   Text    | <ul><li>[x] </li></ul> | Human readable duration based of the field above / Or "live" if show is ongoing <sup><a href="#episodes-origin-4" /> [[4]](#episodes-ref-4)</sup> |
|     flags     |  BigInt   | <ul><li>[x] </li></ul> | An integer encoding the flags listed against an episode, this is decoded to boolean values using [masks available below](#episode-flags)          |
|   stream_id   |   Text    | <ul><li>[ ] </li></ul> | The video ID on CloudFlare's Stream platform (if present) <sup><a href="#episodes-origin-5" /> [[5]](#episodes-ref-5)</sup>                       |
| last_modified | Timestamp | <ul><li>[x] </li></ul> | An ISO8601 timestamp representing the last time a change was made to the entity                                                                   |

### References

- <a href="#episodes-ref-1" /> [[1]](#episodes-origin-1),
  <a href="#episodes-ref-4" /> [[4]](#episodes-origin-4) | This field will be
  getting removed entirely because it is wasteful
- <a href="#episodes-ref-2" /> [[2]](#episodes-origin-2) | This field will be
  converted from a URL to a unique ID and reconstructed on the client side
- <a href="#episodes-ref-3" /> [[3]](#episodes-origin-3) | This field may on
  occasion be out of sync by about 24 hours due to to the delays in VOD
  availability
- <a href="#episodes-ref-5" /> [[5]](#episodes-origin-5) | This field is only
  populated for videos which have a possible "known good" copy and are otherwise
  corrupted

---

# Episode Flags

|        Mask        | Decimal | Flag          | Description                                                                                                                |
| :----------------: | :------ | :------------ | :------------------------------------------------------------------------------------------------------------------------- |
| `0000000000000001` | 1       | Thumb         | Video has a thumbnail hosted on our CDN <sup><a href="#flags-origin-1"> [[1]](#flags-ref-1)</a></sup>                      |
| `0000000000000010` | 2       | AOD           | Video has an AOD / Audio On Demand File (Hosted on our CDN)                                                                |
| `0000000000000100` | 4       | VOD           | Video has an VOD / Video On Demand File (Hosted on our CDN)                                                                |
| `0000000000001000` | 8       | WebVTT        | Video has a transcript file available                                                                                      |
| `0000000000010000` | 16      | Private       | Video is private - These videos are not recognized by the API                                                              |
| `0000000000100000` | 32      | Stream        | Video is available via Stream Player                                                                                       |
| `0000000001000000` | 64      | Live          | Video is currently being actively livestreamed by LMG (This flag should be exclusive!)                                     |
| `0000000010000000` | 128     | Corrupt       | Video is corrupted and users should be warned of this when viewing VOD content.                                            |
| `0000000100000000` | 256     | C/W           | Video has a content warning applied, this is usually because it is an older video before they were so careful about things |
| `0000001000000000` | 512     | Guest         | Video features one or more guests to the show (non LMG staff)                                                              |
| `0000010000000000` | 1,024   | LTX/Trade     | This show was streamed from an LTX or other industry event                                                                 |
| `0000100000000000` | 2,048   | MM            | Video features the use of Merch Messages                                                                                   |
| `0001000000000000` | 4,096   | PL            | Video features the launch of a product by LMG/Creator Warehouse                                                            |
| `0010000000000000` | 8,192   | NEEDTOPIC     | Video needs to be chacked for new topics - Flag remains until the topic count is more than 0                               |
| `0100000000000000` | 16,384  | HAS_WAN_BINGO | Video has an associated WAN Show Bingo instance (spreadsheet?)                                                             |
| `1000000000000000` | 32,768  | Not In Use    | This flag is currently not in use                                                                                          |

### References

- <a href="#flags-ref-1"> [[1]](#flags-origin-1)</a> |
  [See Cloudflare docs](https://developers.cloudflare.com/stream/)
