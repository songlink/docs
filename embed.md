# Embed

Our embed automatically finds and displays links to all the major streaming platforms for any song or album and comes in a variety of sizes. 

To see all of the options and sizes for our embed, check out an example Songlink here: [https://song.link/i/1051394215?embed=1](https://song.link/i/1051394215?embed=1).

## Quickest implementation

Find the song or album you'd like to embed by searching for it on [our web app](https://song.link). Then, on the Songlink page, click the **EMBED** button, located beneath the album art.

You should then see options for customizing the embed, including colors and sizes. Once you've found the one you'd like to use, copy the iframe code and paste it into the HTML of your website.

If you're having issues implementing the code into your website, feel free to reach out to us at [hello@song.link](mailto:hello@song.link) and we'll be happy to help you get set up.

## Full documentation

If you'd like to programmatically or manually create embeds from songs or albums on Spotify, Apple Music, etc, then keep reading.

The Songlink embed is easy to implement via an `<iframe/>` and is implemented similarly to other embed experiences from YouTube and Spotify.

### Implementing the Songlink Embed

To implement our embed to your blog or website, add an `<iframe/>` like this one:

```html
<iframe width="100%" height="150" src="https://embed.song.link/?url=spotify:track:1eQBEelI2NCy7AUTerX0KS&theme=dark" fframeborder="0" allowtransparency allowfullscreen sandbox="allow-same-origin allow-scripts allow-presentation"></iframe>
```

To choose which song or album you want, simply modify the `?url=` parameter of the `src` of the iframe. The `?url=` parameter should be the URL of the song or album you want to embed, e.g. a Spotify track URL. We [support songs and albums from most major streaming platforms](FAQ.md). You can also pass in any valid Songlink URL, such as [https://song.link/s/4sPmO7WMQUAf45kwMOtONw](https://song.link/s/4sPmO7WMQUAf45kwMOtONw).

**NOTE**: You don't necessarily have to, but it's best if you encode these URLs. In JavaScript, you can `encodeURIComponent(url)` before adding it as the `?url=`parameter.

We currently support two themes: light and dark. Simply change the `&theme=` query param to either `light` or `dark` to specify a theme.

Our embed experience will look good in almost all sizes, but we suggest a minimum width of 280px and a minimum height of 52px.

### Embed sizes

There are three types of Songlink Embeds: compact, album, and video.

**SMALL**

The small embed contains all the links to the streaming platforms, as well as a small thumbnail of the album art. This layout is probably best used in support of your current YouTube, Spotify or other embed solution. Many bloggers have added the small embed directly underneath their YouTube embeds.

To render a small embed, make sure the `height` of the `<iframe/>` is `52px`. Here is example code for a Compact Embed:

```html
<iframe width="100%" height="52" src="https://embed.song.link/?url=spotify:track:1eQBEelI2NCy7AUTerX0KS" frameborder="0" allowtransparency allowfullscreen sandbox="allow-same-origin allow-scripts allow-presentation"></iframe>
```

**MEDIUM**

The medium embed is displays the title, artist and album cover, along with the links below. To render this size, set the `height` of the `<iframe/>` between `124px`and `229px`. Here is example code for a medium size embed:

```html
<iframe width="100%" height="150" src="https://embed.song.link/?url=spotify:track:1eQBEelI2NCy7AUTerX0KS" frameborder="0" allowtransparency allowfullscreen sandbox="allow-same-origin allow-scripts allow-presentation"></iframe>
```

**LARGE**

The large ewmbed has it all: a prominent, featured music video supported by links to the song or album on all the major streaming platforms.

To render this size, set the `height` of the `<iframe/>` to be `230px` or larger. Here is an example code:

```html
<iframe width="100%" height="414" src="https://embed.song.link/?url=spotify:track:1eQBEelI2NCy7AUTerX0KS" frameborder="0" allowtransparency allowfullscreen sandbox="allow-same-origin allow-scripts allow-presentation"></iframe>
```

For the large size, we recommend the `height` be `width * 0.5625 + 52` which will render the YouTube video in the correct 9:16 ratio. You can use a parent `<div/>` to help you achieve this, like so:

```html
<div style="max-width:100%;"><div style="position:relative;padding-bottom:calc(56.25% + 52px);height: 0;"><iframe style="position:absolute;top:0;left:0;" width="100%" height="100%" src="https://embed.song.link/?url=https%3A%2F%2Fsong.link%2Fus%2Fi%2F1182062656&theme=dark" frameborder="0" allowfullscreen sandbox="allow-same-origin allow-scripts allow-presentation"></iframe></div></div>
```

## Converting YouTube embeds into Songlink embeds

If you already have a YouTube embed, you can simply prepend `https://embed.song.link/?url=` to the YouTube `src` URL of the `<iframe/>`. For example, if you have a YouTube `<iframe/>` with the following `src` attribute:

```html
<iframe ... src=https://youtube.com/embed/lo4f5CVFGKc ... />
```

You can simply add a little bit of "magic":

```html
<iframe ... src=https://embed.song.link/?url=https://youtube.com/embed/lo4f5CVFGKc ...  />
```

Et voilà, you’ve created a Songlink embed.

## Embedding Songlinks on Medium

If you publish stories on the Medium platform, embedding a Songlink into your next story is as easy as pasting a Songlink URL into the text. Medium will automatically recognize it and convert the link into the embedded experience.

## Questions?

If you have any questions or want some help with integrating our embeds into your website or blog, message us at [hello@song.link](mailto:hello@song.link). 

Happy embedding! 🚀 🙏
