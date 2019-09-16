## FAQ

### Which music services does Songlink support?

There are two types of platforms that Songlink supports: **automated** and **manual**.

The automated platforms we support are: Spotify, Apple Music/iTunes, YouTube, Pandora, Tidal, SoundCloud, Deezer, Google Play Music/Google Play Store, Napster, Amazon Music/Amazon Store, Yandex.Music and Spinrilla. 

These automated platforms will pop up on Songlinks automatically. If our services miss one or get one wrong, please reach out to us at [hello@song.link](mailto:hello@song.link) and we'll make sure it gets fixed. 

We also support many "manual" platforms. These links have to be added manually since the platforms do not allow us to automatically access their catalog. Please reach out to us to let us know if you'd like to add a manual link to your Songlink page.

The manual platforms we support are: Bandcamp, Beatport, MyMixtapez, Datpiff and Live Mixtapes.

We are working on a set of features that will allow you, the user, to more easily add these manual links without having to reach out to us.

Let us know which other platforms you'd like to see on your Songlinks by writing us at [hello@song.link](mailto:hello@song.link). 🙏

### What if the YouTube video is incorrect, or my page is missing links?

We apologize for any incorrect videos or links. Our service (usually) does a great job of automatically finding songs and albums across all the streaming platforms, but sometimes it gets it wrong. 

If you notice an incorrect video or link, please let us know by emailing us at [hello@song.link](mailto:hello@song.link). We can usually get it fixed within a couple hours. 

### Can you upload your music through Songlink?

No, we don't offer this service. 

Songlink automatically aggregates your music across all of the major music streaming platforms, but the song or album must already be uploaded onto at least one of those platforms.

To learn more about how to use Songlink, please refer to [this help article](what-is-songlink.md).

### How do I register or sign up for a Songlink account?

The **good** news: there is no need to sign up or login to Songlink because our service is free for everyone.

The **better** news: we are working on awesome new features, some of which may require you to sign up or log in. So stay tuned. 😄

For more information about how to use Songlink, check out [this help article](what-is-songlink.md).

### How do I customize my Songlink URL?

Our free-to-use Songlinks do not have the nicest URLs. They usually look something like this:

[https://song.link/us/i/1051394215](https://song.link/us/i/1051394215)

You might want to share a shorter, prettier URL, especially if you're sharing it in Instagram or Twitter bios. For this use case, we offer custom URLs that you can create and purchase for $3.99 USD.

To create a custom URL, click on the "Make It Pretty" button on any song or album page. Then, type in the custom URL you want to create for that page and complete the checkout process.

That ugly link above? It can now be something like:

[https://song.link/Hello](https://song.link/Hello)

These custom, pretty links provide an instant connection, drive more attention to the link and better reflect your brand and vibes. 😎

### How can I avoid 429 Too Many Requests error when I add many embeds to my website?

Unfortunately, we must impose rate limits on all of our services because we ourselves have to abide by rate limits from our data sources, e.g. Spotify, YouTube, etc. 

The current rate limit for our embed is 60 per minute per IP address. This means that if you load 61 embeds on a single page, the 61st embed will trigger a 429 error and not load properly. 

If you want to display more than 60 embeds, we suggest breaking them up in some way so they don't all load at the same time. This will also increase the speed of the page load, since the user's browser must load and handle all of the embeds if they all load at the same time. 

There are a couple ways to accomplish this: 

- You can place each embed (or groups of embeds) on their own page or behind a click (so only load the embed after the user clicks to view it). 
- You can "lazy load" the embeds, so that only first few load at first, then once the user scrolls down enough, you load the next group of them. 

There are likely many ways to build this that helps both us and the user provide a smooth experience. Please reach out if you'd like to discuss your specific use case.
