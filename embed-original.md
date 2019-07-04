> **NOTE**: This documentation covers the original, older version of our embed. We are still supporting this embed, and will do so for the foreseeable future, but we will likely not be improving it or adding features to it.

# Embed

The Songlink Embed will aggregate any song or album across all the streaming platforms so all of your readers can engage.

The Songlink Embed allows you to inject the Songlink experience into your blog or website. By aggregating songs and albums across all the major streaming services, the Songlink Embed will ensure that **all** of your readers and users will be able to engage and listen to the music you are discussing.

## Quickest implementation

The easiest way to get the code necessary to add an embed to your website is to head to [home page](https://song.link/) and [find the Songlink you'd like to embed](http://help.song.link/faq/how-do-i-use-songlink). Then, on the Songlink page, click the SHARE button underneath the album art, then click the Embed icon.

A popup should load which will have each of the three different sizes and layouts of embeds we support. Find the one you'd like to use, copy the embed code and paste it into the HTML of your website.

If you're having issues implementing the code into your website, feel free to reach out to us at [hello@song.link](mailto:hello@song.link) and we'll be happy to help you get set up.

## Full documentation

The following documentation describes how to compose embed codes for any song or album. If you'd like to programmatically or automatically create embeds from songs or albums on Spotify, Apple Music, etc, then keep reading.

The Songlink Embed code is easy to implement via an `<iframe/>` and is similar to other embed experiences from YouTube and Spotify.

## Implementing the Songlink Embed

To implement a Songlink Embed to your blog or website, add an `<iframe/>` like this one:

```html
<iframe width="480" height="199" src="https://song.link/embed?url=spotify:track:1eQBEelI2NCy7AUTerX0KS" frameborder="0" allowtransparency allowfullscreen></iframe>
```

To choose which song or album you want, simply modify the `?url=` parameter of the `src`. The `?url=` parameter should be the URL of the song or album you want to embed. We support song and album URLs from Spotify, Apple Music, YouTube, SoundCloud, Google Play Music, Tidal and Deezer. You can also pass in any valid Songlink URL, such as [https://song.link/s/4sPmO7WMQUAf45kwMOtONw](https://song.link/s/4sPmO7WMQUAf45kwMOtONw).

**NOTE**: You don't necessarily have to, but it's best if you encode these URLs. In JavaScript, you can `encodeURIComponent(url)` before adding it as the `?url=` parameter.

Our embed experience will look good in almost all sizes, but we suggest a minimum width of 280px and a minimum height of 88px.

## Different Songlink Embed Layouts

There are three types of Songlink Embeds: compact, album, and video.

### Compact Embed

The Compact Embed contains only the listen, buy and share icons. This layout is probably best used in support of your current YouTube, Spotify or other embed solution. Many bloggers have added the Compact Embed directly underneath their YouTube embeds.

To render a Compact Embed, set the `height` of the `<iframe/>` to be `128px` or less, but no smaller than `88px`. Here is example code for a Compact Embed:

```html
<iframe width="560" height="99" src="https://song.link/embed?url=spotify:track:1eQBEelI2NCy7AUTerX0KS" frameborder="0" allowtransparency allowfullscreen></iframe>
```

Since the Compact Embed has no identifying information about the song or album, we recommend you use it beneath and in support of other embeddable experiences from YouTube, Spotify, etc.

### Cover Art

The Cover Art Embed is slightly taller and it displays the title, artist and album cover. It’s also the default layout if there isn’t a YouTube video for the song you’re sharing.

To render a Cover Art Embed, set the `height` of the `<iframe/>` to be between `129px`and `199px`. Here is example code for a Cover Art Embed:

```html
<iframe width="560" height="199" src="https://song.link/embed?url=spotify:track:1eQBEelI2NCy7AUTerX0KS" frameborder="0" allowtransparency allowfullscreen></iframe>
```

### Video

The Video Embed has it all: a prominent, featured music video supported by links to the song or album on all the major streaming platforms.

To render a Video Embed, set the `height` of the `<iframe/>` to be `200px` or larger. Here is example code for a Video Songlink Embed:

```html
<iframe width="560" height="414" src="https://song.link/embed?url=spotify:track:1eQBEelI2NCy7AUTerX0KS" frameborder="0" allowtransparency allowfullscreen></iframe>
```

For a Video Songlink Embed, we recommend the `height` be `width * 0.5625 + 88`, but the Video Songlink Embed will look pretty good in many aspect ratios, including the 9:16 ratio that is used by YouTube embeds.

## Converting YouTube embeds into Songlink Embed

If you already have a YouTube embed, you can simply prepend `https://song.link/embed?url=` to the YouTube `src` URL of the `<iframe/>`. For example, if you have a YouTube `<iframe/>` with the following `src` attribute:

```html
src=https://youtube.com/embed/lo4f5CVFGKc
```

You can simply add a little bit of Songlink magic:

```html
src=https://song.link/embed?url=https://youtube.com/embed/lo4f5CVFGKc
```

Et voilà, you’ve created a Songlink Embed.

## **Embedding Songlinks on Medium**

If you write stories using the Medium platform, embedding a Songlink into your next story is as easy as pasting a Songlink URL into the text. Medium will automatically recognize it and convert the link into the embedded experience.

## **Questions?**

If you have any questions or want some help with integrating the Songlink Embed into your website or blog, email us at [hello@song.link](mailto:hello@song.link).
