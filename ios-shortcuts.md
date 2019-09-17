# iOS Shortcuts

We know of a few iOS Shortcuts via the [Shortcuts app](https://apps.apple.com/us/app/shortcuts/id915249334) that can be handy for creating and sharing Songlinks. If you have a specific use case, these might be great starting points for building your own.

### [Go To Songlink](https://www.icloud.com/shortcuts/5c1c62adcec7451bad67badaf8bd2ea7)

This one will load the Songlink page in your browser.

**How To Use**: Streaming app song or album (e.g. Spotify) > Share > Shortcuts > Go To Songlink (this shortcut) > Songlink page opens

### [Share Short Songlink URL](https://www.icloud.com/shortcuts/0e21347504df41519fbd2c9ffaab73d1)

This one will copy the short Songlink URL, e.g. https://song.link/s/1GZH9Sv6zCIse2GKihRHKy, to the clipboard and open up the share dialog so you can share it.

**How To Use**: Streaming app song or album (e.g. Spotify) > Share > Shortcuts > Share Short Songlink URL (this shortcut) > Share

This one queries our API in order to get the shortened version of the URL. If you have a specific use case, e.g. you want a shortcut to always open the song or album in Apple Music, you can duplicate and tweak this shortcut and parse whatever data you need from our API response. Information about the data in our API response can be found [here](https://github.com/songlink/docs/blob/master/api-v1-alpha.1.md#response-structuretypes).

### [Share Long Songlink URL](https://www.icloud.com/shortcuts/ab6e3c8ec1dc4d6dace7709da863eb7a)

This one will copy the long Songlink URL, e.g. https://song.link/https://open.spotify.com/track/1GZH9Sv6zCIse2GKihRHKy, to the clipboard and open up the share dialog so you can share it. This one is faster than "Share Short Songlink URL" because it doesn't query our API, but the URL is longer and a bit uglier.

**How To Use**: Streaming app song or album (e.g. Spotify) > Share > Shortcuts > Share Long Songlink URL (this shortcut) > Share

### [Share Songlink URL From Apple Music Now Playing](https://www.icloud.com/shortcuts/c6d7aba0ffb84fa5a29b8cd540a03a3d)

This one is initiated from the Shortcuts app. If there's a song playing in Apple Music, it will grab the Songlink URL and share it.

**How To Use**: Shortcuts app > Share Songlink URL From Apple Music Now Playing (this shortcut) > Share
