# API Documentation (v1-alpha.1)

Information, documentation for Songlink's public API, currently on version 1-alpha.1.

## What is an alpha release?

I'm not sure. 😅 This is our first attempt at opening up our data with an API, so I suspect we'll want to improve things as we learn about how developers use it or want to use it. We've labeled this as an "alpha" version meaning things may break or change, but we'll do our best to communicate those changes.

Please don't hesitate to reach out to us at [developers@song.link](mailto:developers@song.link) with feedback or suggestions. 

## Versioning

This is the documentation for Songlink API version 1-alpha.1. The API request and response structures may change. In the case of breaking changes, a new version of the API will be supported.

Requests to the API should specify the version of the API you'd like to consume:

```bash
curl -X GET "https://api.song.link/{{VERSION}}/links?..."
```

e.g. for v1-alpha.1:

```bash
curl -X GET "https://api.song.link/v1-alpha.1/links?..."
```

## Attribution

Please properly attribute your integration with our API by displaying to your users that your feature or product is powered by Songlink. We're really flexible on this; if you have any questions or concerns please reach out to us at [developers@song.link](mailto:developers@song.link).

## Terms of Service

Use of our API is governed by our [API Terms of Service](https://song.link/api-terms).

## Auth
You do not need any special authentication or authorization for our API. However, if you do provide a valid API key you will benefit from higher rate limits and preferred support. If interested, [send us an email](mailto:developers@song.link) and we'll send you an API key. Then, add it as the key query param, like so: 

```bash
curl -X GET "https://api.song.link/v1-alpha.1/links?url=spotify%3Atrack%3A0Jcij1eWd5bDMU5iPbxe2i&userCountry=US&key=9ed95450-2b6f-4aae-a3ab-34b6bca4f786"
```

## Rate Limiting

Without an API key, the rate limit is 10 requests per minute. The rate limit with an API key is 60 requests per minute. If you need to increase this limit, let us know. We'd love to learn more about your use case and increase the rate limit for your API key. 

## Supported platforms

We recognize and can match entities from the following platforms:

```
spotify
itunes
appleMusic
youtube
youtubeMusic
google
googleStore
pandora
deezer
tidal
amazonStore
amazonMusic
soundcloud
napster
yandex
spinrilla
```

## `GET /links` endpoint

This is the main (and right now, only) 😅 endpoint that allows you to fetch the matching links for a given streaming entity. For example, with this endpoint you can provide the URL of an Apple Music track and receive the URLs and data for that song on Spotify, YouTube, Tidal and more.

### Example request

Replace <key> with your API key. 

```bash
curl -X GET "https://api.song.link/v1-alpha.1/links?url=spotify%3Atrack%3A0Jcij1eWd5bDMU5iPbxe2i&userCountry=US&key=<key>"
```

### Query Params

**`url`** -- The URL of a valid song or album from any of our supported platforms. It is safest to encode the URL, e.g. with `encodeURIComponent()` 

**`userCountry`** -- Two-letter country code. Specifies the country/location we use when searching streaming catalogs. Optional. Defaults to `US`.

**`platform`** -- The platform of the entity you'd like to match. See above section for supported platforms. If `url` is not provided, you must provide `platform`, `type` and `id`.

**`type`** -- The type of streaming entity. We support `song` and `album`. If `url` is not provided, you must provide `platform`, `type` and `id`.

**`id`** -- The unique identifier of the streaming entity, e.g. `1443109064` which is an iTunes ID. If `url` is not provided, you must provide `platform`, `type` and `id`.

### Response Structure/Types

```js
// @flow

type Response = {
  // The unique ID for the input entity that was supplied in the request. The
  // data for this entity, such as title, artistName, etc. will be found in
  // an object at `nodesByUniqueId[entityUniqueId]`
  entityUniqueId: string,

  // The userCountry query param that was supplied in the request. It signals
  // the country/availability we use to query the streaming platforms. Defaults
  // to 'US' if no userCountry supplied in the request.
  //
  // NOTE: As a fallback, our service may respond with matches that were found
  // in a locale other than the userCountry supplied
  userCountry: string,

  // A URL that will render the Songlink page for this entity
  pageUrl: string,

  // A collection of objects. Each key is a platform, and each value is an
  // object that contains data for linking to the match
  linksByPlatform: {
    // Each key in `linksByPlatform` is a Platform. A Platform will exist here
    // only if there is a match found. E.g. if there is no YouTube match found,
    // then neither `youtube` or `youtubeMusic` properties will exist here
    [Platform]: {
      // The unique ID for this entity. Use it to look up data about this entity
      // at `entitiesByUniqueId[entityUniqueId]`
      entityUniqueId: string,

      // The URL for this match
      url: string,

      // The native app URI that can be used on mobile devices to open this
      // entity directly in the native app
      nativeAppUriMobile?: string,

      // The native app URI that can be used on desktop devices to open this
      // entity directly in the native app
      nativeAppUriDesktop?: string,
    },
  },

  // A collection of objects. Each key is a unique identifier for a streaming
  // entity, and each value is an object that contains data for that entity,
  // such as `title`, `artistName`, `thumbnailUrl`, etc.
  entitiesByUniqueId: {
    [entityUniqueId]: {
      // This is the unique identifier on the streaming platform/API provider
      id: string,

      type: 'song' | 'album',

      title?: string,
      artistName?: string,
      thumbnailUrl?: string,
      thumbnailWidth?: number,
      thumbnailHeight?: number,

      // The API provider that powered this match. Useful if you'd like to use
      // this entity's data to query the API directly
      apiProvider: APIProvider,

      // An array of platforms that are "powered" by this entity. E.g. an entity
      // from Apple Music will generally have a `platforms` array of
      // `["appleMusic", "itunes"]` since both those platforms/links are derived
      // from this single entity
      platforms: Platform[],
    },
  },
};

type Platform =
  | 'spotify'
  | 'itunes'
  | 'appleMusic'
  | 'youtube'
  | 'youtubeMusic'
  | 'google'
  | 'googleStore'
  | 'pandora'
  | 'deezer'
  | 'tidal'
  | 'amazonStore'
  | 'amazonMusic'
  | 'soundcloud'
  | 'napster'
  | 'yandex'
  | 'spinrilla';

type APIProvider =
  | 'spotify'
  | 'itunes'
  | 'youtube'
  | 'google'
  | 'pandora'
  | 'deezer'
  | 'tidal'
  | 'amazon'
  | 'soundcloud'
  | 'napster'
  | 'yandex'
  | 'spinrilla';

```

### Why the weird keys in `entitiesByUniqueId`?
Great question. 😅 After working with this data internally for a couple years, this is the structure we've landed on as being the most scalable and flexible. Admittedly, I'm still working on explaining it concisely and precisely, but here goes:

The keys in `linksByPlatform` are constants, which is easier than the dynamic keys in `entitiesByUniqueId`. We chose constants here for two reasons:

1. The links are the main data (I think) that most developers want, so this makes accessing it easier.

2. The point of `linksByPlatform` (as of right now) is that we find exactly one match per platform. However, one-link-per-platform not be sustainable in the long-term. For instance, what happens when we get more advanced and find all the matches for a given platform, e.g. the YouTube official music video as well as the YouTube Music generic track/video? We'll probably have to make the values in `linksByPlatform` arrays (or possibly make new platform keys, e.g. `youtubeOfficialVideo`).

Now, if we use constant keys for `entitiesByUniqueId`, similar to `linksByPlatform`, then what would we do in cases where a single entity is powered by/represented by multiple links/platforms, e.g. YouTube and YouTube Music? Would we have just one entity at the key `youtube`? Or would we also have a key for `youtubeMusic`, which will often be the exact same entity as `youtube`? This would lead to data being duplicated across multiple keys. 

It's also possible the underlying entity is not the same, and this is definitely something we'll be doing more in the future as we advance our matching capabilities. The current strategy of `entitiesByUniqueId` will work well here by containing the data for non-duplicated, unique entities that can then be referenced or "power" other data we care about, e.g. `linksByPlatform`. This allows a single YouTube entity, e.g. `YOUTUBE_VIDEO::123` to power both `youtube` and `youtubeMusic` properties in `linksByPlatform`, but also allows us to have two distinct entities powering these platforms, e.g. `YOUTUBE_VIDEO::123` is the official video for the `youtube` link and `YOUTUBE_VIDEO::456` is the auto-generated video more suitable for the `youtubeMusic` link.

### Example Response

```json
{
    "entityUniqueId": "ITUNES_SONG::1443109064",
    "userCountry": "US",
    "pageUrl": "https://song.link/us/i/1443109064",
    "entitiesByUniqueId": {
        "ITUNES_SONG::1443109064": {
            "id": "1443109064",
            "type": "song",
            "title": "Kitchen",
            "artistName": "Kid Cudi",
            "thumbnailUrl": "https://is4-ssl.mzstatic.com/image/thumb/Music118/v4/ac/2c/60/ac2c60ad-14c3-a8b2-d962-dc08de2da546/source/512x512bb.jpg",
            "thumbnailWidth": 512,
            "thumbnailHeight": 512,
            "apiProvider": "itunes",
            "platforms": [
                "appleMusic",
                "itunes"
            ]
        },
        "SPOTIFY_SONG::0Jcij1eWd5bDMU5iPbxe2i": {
            "id": "0Jcij1eWd5bDMU5iPbxe2i",
            "type": "song",
            "title": "Kitchen",
            "artistName": "Kid Cudi",
            "thumbnailUrl": "https://i.scdn.co/image/477884e59cbdf2b7ff2cae31d57f0a7b2fde1b97",
            "thumbnailWidth": 640,
            "thumbnailHeight": 640,
            "apiProvider": "spotify",
            "platforms": [
                "spotify"
            ]
        },
        "YOUTUBE_VIDEO::w3LJ2bDvDJs": {
            "id": "w3LJ2bDvDJs",
            "type": "song",
            "title": "Kitchen",
            "artistName": "Kid Cudi",
            "thumbnailUrl": "https://i.ytimg.com/vi/w3LJ2bDvDJs/hqdefault.jpg",
            "thumbnailWidth": 480,
            "thumbnailHeight": 360,
            "apiProvider": "youtube",
            "platforms": [
                "youtube",
                "youtubeMusic"
            ]
        },
        "GOOGLE_SONG::Tj3j7gin3skidcsqsqdzdxxr6t4": {
            "id": "Tj3j7gin3skidcsqsqdzdxxr6t4",
            "type": "song",
            "title": "Kitchen",
            "artistName": "Kid Cudi",
            "thumbnailUrl": "https://lh3.googleusercontent.com/3cs-Hry0V8Au2vLTXXLBpEQH66WLK__NU_96XAhtYbF-ptOyPzutiH1OS4aWJj6NnWyInuJGQw",
            "thumbnailWidth": 512,
            "thumbnailHeight": 512,
            "apiProvider": "google",
            "platforms": [
                "google",
                "googleStore"
            ]
        },
        "PANDORA_SONG::TR:13075840": {
            "id": "TR:13075840",
            "type": "song",
            "title": "Kitchen",
            "artistName": "Kid Cudi",
            "thumbnailUrl": "https://content-images.p-cdn.com/images/public/int/5/8/6/1/00602557251685_500W_500H.jpg",
            "thumbnailWidth": 500,
            "thumbnailHeight": 500,
            "apiProvider": "pandora",
            "platforms": [
                "pandora"
            ]
        },
        "DEEZER_SONG::138127073": {
            "id": "138127073",
            "type": "song",
            "title": "Kitchen",
            "artistName": "Kid Cudi",
            "thumbnailUrl": "https://cdns-images.dzcdn.net/images/cover/28c2c4c39bdf3ed9518fdb2c52723cbe/500x500-000000-80-0-0.jpg",
            "thumbnailWidth": 500,
            "thumbnailHeight": 500,
            "apiProvider": "deezer",
            "platforms": [
                "deezer"
            ]
        },
        "AMAZON_SONG::B01NAE38YO": {
            "id": "B01NAE38YO",
            "type": "song",
            "title": "Kitchen",
            "artistName": "Kid Cudi",
            "thumbnailUrl": "https://images-na.ssl-images-amazon.com/images/I/41F-Bf2dLrL.jpg",
            "thumbnailWidth": 500,
            "thumbnailHeight": 500,
            "apiProvider": "amazon",
            "platforms": [
                "amazonMusic",
                "amazonStore"
            ]
        },
        "TIDAL_SONG::67784545": {
            "id": "67784545",
            "type": "song",
            "title": "Kitchen",
            "artistName": "Kid Cudi",
            "thumbnailUrl": "https://resources.tidal.com/images/a660376f/4fba/400a/9f8b/da00f7cab11e/640x640.jpg",
            "thumbnailWidth": 640,
            "thumbnailHeight": 640,
            "apiProvider": "tidal",
            "platforms": [
                "tidal"
            ]
        },
        "NAPSTER_SONG::tra.246588040": {
            "id": "tra.246588040",
            "type": "song",
            "title": "Kitchen",
            "artistName": "Kid Cudi",
            "thumbnailUrl": "https://direct.rhapsody.com/imageserver/images/alb.246588025/385x385.jpeg",
            "thumbnailWidth": 385,
            "thumbnailHeight": 385,
            "apiProvider": "napster",
            "platforms": [
                "napster"
            ]
        },
        "YANDEX_SONG::32504596": {
            "id": "32504596",
            "type": "song",
            "title": "Kitchen",
            "artistName": "Kid Cudi",
            "thumbnailUrl": "https://avatars.yandex.net/get-music-content/38044/2ce3bc1b.a.3962211-1/600x600",
            "thumbnailWidth": 600,
            "thumbnailHeight": 600,
            "apiProvider": "yandex",
            "platforms": [
                "yandex"
            ]
        }
    },
    "linksByPlatform": {
        "appleMusic": {
            "url": "https://music.apple.com/us/album/kitchen/1443108737?i=1443109064&uo=4&app=music&ls=1&at=1000lHKX",
            "nativeAppUriMobile": "music://music.apple.com/us/album/kitchen/1443108737?i=1443109064&uo=4&app=music&ls=1&at=1000lHKX",
            "nativeAppUriDesktop": "itms://music.apple.com/us/album/kitchen/1443108737?i=1443109064&uo=4&app=music&ls=1&at=1000lHKX",
            "entityUniqueId": "ITUNES_SONG::1443109064"
        },
        "spotify": {
            "url": "https://open.spotify.com/track/0Jcij1eWd5bDMU5iPbxe2i",
            "nativeAppUriDesktop": "spotify:track:0Jcij1eWd5bDMU5iPbxe2i",
            "entityUniqueId": "SPOTIFY_SONG::0Jcij1eWd5bDMU5iPbxe2i"
        },
        "youtube": {
            "url": "https://www.youtube.com/watch?v=w3LJ2bDvDJs",
            "entityUniqueId": "YOUTUBE_VIDEO::w3LJ2bDvDJs"
        },
        "youtubeMusic": {
            "url": "https://music.youtube.com/watch?v=w3LJ2bDvDJs",
            "entityUniqueId": "YOUTUBE_VIDEO::w3LJ2bDvDJs"
        },
        "google": {
            "url": "https://play.google.com/music/m/Tj3j7gin3skidcsqsqdzdxxr6t4?signup_if_needed=1",
            "entityUniqueId": "GOOGLE_SONG::Tj3j7gin3skidcsqsqdzdxxr6t4"
        },
        "pandora": {
            "url": "https://www.pandora.com/artist/kid-cudi/passion-pain-and-demon-slayin/kitchen/TRptv2hl5r9m5hV",
            "entityUniqueId": "PANDORA_SONG::TR:13075840"
        },
        "deezer": {
            "url": "https://www.deezer.com/track/138127073",
            "entityUniqueId": "DEEZER_SONG::138127073"
        },
        "amazonMusic": {
            "url": "https://music.amazon.com/albums/B01N48U32A?trackAsin=B01NAE38YO&do=play",
            "entityUniqueId": "AMAZON_SONG::B01NAE38YO"
        },
        "tidal": {
            "url": "https://listen.tidal.com/track/67784545",
            "entityUniqueId": "TIDAL_SONG::67784545"
        },
        "napster": {
            "url": "http://napster.com/artist/art.19296515/album/alb.246588025/track/tra.246588040",
            "entityUniqueId": "NAPSTER_SONG::tra.246588040"
        },
        "yandex": {
            "url": "https://music.yandex.ru/track/32504596",
            "entityUniqueId": "YANDEX_SONG::32504596"
        },
        "itunes": {
            "url": "https://music.apple.com/us/album/kitchen/1443108737?i=1443109064&uo=4&app=itunes&ls=1&at=1000lHKX",
            "nativeAppUriMobile": "itms://music.apple.com/us/album/kitchen/1443108737?i=1443109064&uo=4&app=itunes&ls=1&at=1000lHKX",
            "nativeAppUriDesktop": "itms://music.apple.com/us/album/kitchen/1443108737?i=1443109064&uo=4&app=itunes&ls=1&at=1000lHKX",
            "entityUniqueId": "ITUNES_SONG::1443109064"
        },
        "googleStore": {
            "url": "https://play.google.com/store/music/album?id=B7xsarspqwsinxzont6zdvd2hny&tid=song-Tj3j7gin3skidcsqsqdzdxxr6t4",
            "entityUniqueId": "GOOGLE_SONG::Tj3j7gin3skidcsqsqdzdxxr6t4"
        },
        "amazonStore": {
            "url": "https://www.amazon.com/Kitchen/dp/B01NAE38YO?SubscriptionId=AKIAJRL4NME2ROVJ4Q5Q&tag=songlink0d-20&linkCode=xm2&camp=2025&creative=165953&creativeASIN=B01NAE38YO",
            "entityUniqueId": "AMAZON_SONG::B01NAE38YO"
        }
    }
}
```

## Error Codes

We use conventional HTTP response codes to indicate the success or failure of an API request. In general: codes in the `2xx` range indicate success. Codes in the `4xx` range indicate an error that failed given the information provided (e.g., a required parameter was omitted, an incorrect or stale entity URL was provided, etc.). Codes in the 5xx range indicate an error with Songlink's servers.
