### Redirect URLs

We support "redirect URLs" which do not load the Songlink page, but instead redirect the user to a specific music streaming service, as defined by the `to` query param. A Songlink redirect URL can be composed easily with the following format:

```
https://song.link/redirect?url=encodedUrl&to=streamingService
```

More info about each query param:

**`url`**: the URL of the streaming entity, e.g. a spotify song URL. It's best if it's encoded, but it can be the plain URL, too. If using JavaScript or Node.js you can use `encodeURIComponent()`

**`to`**: the streaming service to which you'd like to redirect the user. Can be one of: `spotify`, `appleMusic`, `youtube`, `youtubeMusic`, `google`, `pandora`, `deezer`, `tidal`, `amazonMusic`, `soundcloud`, `napster`, `yandex`, `spinrilla`, `itunes`, `googleStore` or `amazonStore`. If the song is not available in the user's country on the specified streaming service, the Songlink page will load instead.

Here's an example redirect URL:

[https://song.link/redirect?url=https%3A%2F%2Fitun.es%2Fus%2F5Gb0-%3Fi%3D1053825088&to=spotify](https://song.link/redirect?url=https%3A%2F%2Fitun.es%2Fus%2F5Gb0-%3Fi%3D1053825088&to=spotify)

The "input" provided was the Apple Music track [https://itun.es/us/5Gb0-?i=1053825088](https://itun.es/us/5Gb0-?i=1053825088) and it redirects the user to said track on Spotify.
