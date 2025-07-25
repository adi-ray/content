---
title: HTML video and audio
short-title: Video and audio
slug: Learn_web_development/Core/Structuring_content/HTML_video_and_audio
page-type: tutorial-chapter
sidebar: learnsidebar
---

{{PreviousMenuNext("Learn_web_development/Core/Structuring_content/HTML_images", "Learn_web_development/Core/Structuring_content/Mozilla_splash_page", "Learn_web_development/Core/Structuring_content")}}

Now that we are comfortable with adding simple images to a webpage, the next step is to start adding video and audio players to your HTML documents! In this article we'll look at doing just that with the {{htmlelement("video")}} and {{htmlelement("audio")}} elements; we'll then finish off by looking at how to add captions/subtitles to your videos.

<table>
  <tbody>
    <tr>
      <th scope="row">Prerequisites:</th>
      <td>
        Basic HTML familiarity, as covered in
        <a href="/en-US/docs/Learn_web_development/Core/Structuring_content/Basic_HTML_syntax"
          >Basic HTML Syntax</a
        >. Text-level semantics such as <a href="/en-US/docs/Learn_web_development/Core/Structuring_content/Headings_and_paragraphs"
          >headings and paragraphs</a
        > and <a href="/en-US/docs/Learn_web_development/Core/Structuring_content/Lists"
          >lists</a
        >.
      </td>
    </tr>
    <tr>
      <th scope="row">Learning outcomes:</th>
      <td>
        <ul>
          <li>Basic <code>&lt;video&gt;</code> and <code>&lt;audio&gt;</code> tag syntax</li>
          <li>Video and audio-specific attributes such as controls and muted.</li>
          <li>Using <code>&lt;source&gt;</code> elements to provide different video or audio sources.</li>
          <li>The basics of using text tracks such as captions and subtitles.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

## Video and audio on the web

The first influx of online videos and audio were made possible by proprietary plugin-based technologies like [Flash](https://en.wikipedia.org/wiki/Adobe_Flash) and [Silverlight](https://en.wikipedia.org/wiki/Microsoft_Silverlight). Both of these had security and accessibility issues, and are now obsolete, in favor of native HTML solutions {{htmlelement("video")}} and {{htmlelement("audio")}} elements and the availability of {{Glossary("JavaScript")}} {{Glossary("API","APIs")}} for controlling them. We'll not be looking at JavaScript here — just the basic foundations that can be achieved with HTML.

We won't be teaching you how to produce audio and video files — that requires a completely different skill set. We have provided you with [sample audio and video files and example code](https://github.com/mdn/learning-area/tree/main/html/multimedia-and-embedding/video-and-audio-content) for your own experimentation, in case you are unable to get hold of your own.

> [!NOTE]
> Before you begin here, you should also know that there are quite a few OVPs (online video providers) like [YouTube](https://www.youtube.com/), [Dailymotion](https://www.dailymotion.com/), and [Vimeo](https://vimeo.com/), and online audio providers like [Soundcloud](https://soundcloud.com/). Such companies offer a convenient, easy way to host and consume videos, so you don't have to worry about the enormous bandwidth consumption. OVPs even usually offer ready-made code for embedding video/audio in your webpages; if you use that route, you can avoid some of the difficulties we discuss in this article. We'll be discussing this kind of service a bit more in the next article.

## The \<video> element

The {{htmlelement("video")}} element allows you to embed a video very easily. A really simple example looks like this:

```html
<video src="rabbit320.webm" controls>
  <p>
    Your browser doesn't support HTML video. Here is a
    <a href="rabbit320.webm">link to the video</a> instead.
  </p>
</video>
```

The features to note are:

- [`src`](/en-US/docs/Web/HTML/Reference/Elements/video#src)
  - : In the same way as for the {{htmlelement("img")}} element, the `src` (source) attribute contains a path to the video you want to embed. It works in exactly the same way.
- [`controls`](/en-US/docs/Web/HTML/Reference/Elements/video#controls)
  - : Users must be able to control video and audio playback (it's especially critical for people who have [epilepsy](https://en.wikipedia.org/wiki/Epilepsy#Epidemiology).) You must either use the `controls` attribute to include the browser's own control interface, or build your interface using the appropriate [JavaScript API](/en-US/docs/Web/API/HTMLMediaElement). At a minimum, the interface must include a way to start and stop the media, and to adjust the volume.
- The paragraph inside the `<video>` tags
  - : This is called **fallback content** — this will be displayed if the browser accessing the page doesn't support the `<video>` element, allowing us to provide a fallback for older browsers. This can be anything you like; in this case, we've provided a direct link to the video file, so the user can at least access it some way regardless of what browser they are using.

The embedded video will look something like this:

![A simple video player showing a video of a small white rabbit](simple-video.png)

You can [try the example live](https://mdn.github.io/learning-area/html/multimedia-and-embedding/video-and-audio-content/simple-video.html) here (see also the [source code](https://github.com/mdn/learning-area/blob/main/html/multimedia-and-embedding/video-and-audio-content/simple-video.html).)

## Using multiple source formats to improve compatibility

There's a problem with the above example. It is possible that the video might not play for you, because different browsers support different video (and audio) formats. Fortunately, there are things you can do to help prevent this from being an issue.

### Contents of a media file

First, let's go through the terminology quickly. Formats like OGG, WAV, MP4 and WebM are called **[container formats](/en-US/docs/Web/Media/Guides/Formats/Containers)**. They define a structure in which the audio and/or video tracks that make up the media are stored, along with metadata describing the media, what codecs are used to encode its channels, and so forth.

A WebM file containing a movie which has a main video track and one alternate angle track, plus audio for both English and Spanish, in addition to audio for an English commentary track can be conceptualized as shown in the diagram below. Also included are text tracks containing closed captions for the feature film, Spanish subtitles for the film, and English captions for the commentary.

![Diagram conceptualizing the contents of a media file at the track level.](containersandtracks.png)

The audio and video tracks within the container hold data in the appropriate format for the codec used to encode that media. Different formats are used for audio tracks versus video tracks. Each audio track is encoded using an [audio codec](/en-US/docs/Web/Media/Guides/Formats/Audio_codecs), while video tracks are encoded using (as you probably have guessed) [a video codec](/en-US/docs/Web/Media/Guides/Formats/Video_codecs). As we talked about before, different browsers support different video and audio formats, and different container formats (like OGG, MP4, and WebM, which in turn can contain different types of video and audio).

For example:

- A WebM container typically packages Vorbis or Opus audio with VP8/VP9 video. This is supported in all modern browsers, though older versions may not work.
- An MP4 container often packages AAC or MP3 audio with H.264 video. This is also supported in all modern browsers.
- The Ogg container tends to use Vorbis audio and Theora video. This is best supported in Firefox and Chrome, but has basically been superseded by the better quality WebM format.

There are some special cases. For example, for some types of audio, a codec's data is often stored without a container, or with a simplified container. One such instance is the FLAC codec, which is stored most commonly in FLAC files, which are just raw FLAC tracks.

Another example is the ever-popular "MP3 file". An "MP3 file" is an audio file encoded using MPEG-1 Audio Layer III compression. While it can include metadata, it is not encapsulated within a separate MPEG or MPEG-2 container. Its widespread support in the {{htmlelement("audio")}} and {{htmlelement("video")}} elements is largely a testament to its enduring popularity.

An audio player will tend to play an audio track directly, e.g., an MP3 or Ogg file. These don't need containers.

### Media file support in browsers

> [!NOTE]
> Several popular formats, such as MP3 and MP4/H.264, are excellent but are encumbered by patents; that is, there are patents covering some or all of the technology that they're based upon. In the United States, patents covered MP3 until 2017, and H.264 is encumbered by patents through at least 2027.
>
> Because of those patents, browsers that wish to implement support for those codecs must pay typically enormous license fees. In addition, some people prefer to avoid restricted software and prefer to use only open formats. Due to these legal and preferential reasons, web developers find themselves having to support multiple formats to provide a video experience to their entire audience.

The codecs described in the previous section exist to compress video and audio into manageable files, since raw audio and video are both exceedingly large. Each web browser supports an assortment of **{{Glossary("Codec","codecs")}}**, like Vorbis or H.264, which are used to convert the compressed audio and video into binary data and back. Each codec offers its own advantages and drawbacks, and each container may also offer its own positive and negative features affecting your decisions about which to use.

Things become slightly more complicated because not only does each browser support a different set of container file formats, they also each support a different selection of codecs. In order to maximize the likelihood that your website or app will work on a user's browser, you may need to provide each media file you use in multiple formats. If your site and the user's browser don't share a media format in common, your media won't play.

Due to the intricacies of ensuring your app's media is viewable across every combination of browsers, platforms, and devices you wish to reach, choosing the best combination of codecs and container can be a complicated task. See [Choosing the right container](/en-US/docs/Web/Media/Guides/Formats/Containers#choosing_the_right_container) for help selecting the container file format best suited for your needs; similarly, see [Choosing a video codec](/en-US/docs/Web/Media/Guides/Formats/Video_codecs#choosing_a_video_codec) and [Choosing an audio codec](/en-US/docs/Web/Media/Guides/Formats/Audio_codecs#choosing_an_audio_codec) for help selecting the first media codecs to use for your content and your target audience.

One additional thing to keep in mind: mobile browsers may support additional formats not supported by their desktop equivalents, just like they may not support all the same formats the desktop version does. On top of that, both desktop and mobile browsers _may_ be designed to offload handling of media playback (either for all media or only for specific types it can't handle internally). This means media support is partly dependent on what software the user has installed.

So how do we do this? Take a look at the following [updated example](https://github.com/mdn/learning-area/blob/main/html/multimedia-and-embedding/video-and-audio-content/multiple-video-formats.html) ([try it live here](https://mdn.github.io/learning-area/html/multimedia-and-embedding/video-and-audio-content/multiple-video-formats.html), also):

```html
<video controls>
  <source src="rabbit320.mp4" type="video/mp4" />
  <source src="rabbit320.webm" type="video/webm" />
  <p>
    Your browser doesn't support this video. Here is a
    <a href="rabbit320.mp4">link to the video</a> instead.
  </p>
</video>
```

Here we've taken the `src` attribute out of the actual {{HTMLElement("video")}} tag, and instead included separate {{htmlelement("source")}} elements that point to their own sources. In this case the browser will go through the {{HTMLElement("source")}} elements and play the first one that it has the codec to support. Including WebM and MP4 sources should be enough to play your video on most platforms and browsers these days.

Each `<source>` element also has a [`type`](/en-US/docs/Web/HTML/Reference/Elements/source#type) attribute. This is optional, but it is advised that you include it. The `type` attribute contains the {{glossary("MIME type")}} of the file specified by the `<source>`, and browsers can use the `type` to immediately skip videos they don't understand. If `type` isn't included, browsers will load and try to play each file until they find one that works, which obviously takes time and is an unnecessary use of resources.

Refer to our [guide to media types and formats](/en-US/docs/Web/Media/Guides/Formats) for help selecting the best containers and codecs for your needs, as well as to look up the right MIME types to specify for each.

## Other \<video> features

There are a number of other features you can include when displaying an HTML video. Take a look at our next example:

```html
<video
  controls
  width="400"
  height="400"
  autoplay
  loop
  muted
  preload="auto"
  poster="poster.png">
  <source src="rabbit320.mp4" type="video/mp4" />
  <source src="rabbit320.webm" type="video/webm" />
  <p>
    Your browser doesn't support this video. Here is a
    <a href="rabbit320.mp4">link to the video</a> instead.
  </p>
</video>
```

The resulting UI looks something like this:

![A video player showing a poster image before it plays. The poster image says HTML video example, OMG hell yeah!](poster_screenshot_updated.png)

Features include:

- [`width`](/en-US/docs/Web/HTML/Reference/Elements/video#width) and [`height`](/en-US/docs/Web/HTML/Reference/Elements/video#height)
  - : You can control the video size either with these attributes or with {{Glossary("CSS")}}. In both cases, videos maintain their native width-height ratio — known as the **aspect ratio**. If the aspect ratio is not maintained by the sizes you set, the video will grow to fill the space horizontally, and the unfilled space will just be given a solid background color by default.
- [`autoplay`](/en-US/docs/Web/HTML/Reference/Elements/video#autoplay)
  - : Makes the audio or video start playing right away, while the rest of the page is loading. You are advised not to use autoplaying video (or audio) on your sites, because users can find it really annoying.
- [`loop`](/en-US/docs/Web/HTML/Reference/Elements/video#loop)
  - : Makes the video (or audio) start playing again whenever it finishes. This can also be annoying, so only use if really necessary.
- [`muted`](/en-US/docs/Web/HTML/Reference/Elements/video#muted)
  - : Causes the media to play with the sound turned off by default.
- [`poster`](/en-US/docs/Web/HTML/Reference/Elements/video#poster)
  - : The URL of an image which will be displayed before the video is played. It is intended to be used for a splash screen or advertising screen.
- [`preload`](/en-US/docs/Web/HTML/Reference/Elements/video#preload)
  - : Used for buffering large files; it can take one of three values:
    - `"none"` does not buffer the file
    - `"auto"` buffers the media file
    - `"metadata"` buffers only the metadata for the file

You can find the above example available to [play live on GitHub](https://mdn.github.io/learning-area/html/multimedia-and-embedding/video-and-audio-content/extra-video-features.html) (also [see the source code](https://github.com/mdn/learning-area/blob/main/html/multimedia-and-embedding/video-and-audio-content/extra-video-features.html).) Note that we haven't included the `autoplay` attribute in the live version — if the video starts to play as soon as the page loads, you don't get to see the poster!

## The \<audio> element

The {{htmlelement("audio")}} element works just like the {{htmlelement("video")}} element, with a few small differences as outlined below. A typical example might look like so:

```html
<audio controls>
  <source src="viper.mp3" type="audio/mp3" />
  <source src="viper.ogg" type="audio/ogg" />
  <p>
    Your browser doesn't support this audio file. Here is a
    <a href="viper.mp3">link to the audio</a> instead.
  </p>
</audio>
```

This produces something like the following in a browser:

![A simple audio player with a play button, timer, volume control, and progress bar](audio-player.png)

> [!NOTE]
> You can [run the audio demo live](https://mdn.github.io/learning-area/html/multimedia-and-embedding/video-and-audio-content/multiple-audio-formats.html) on GitHub (also see the [audio player source code](https://github.com/mdn/learning-area/blob/main/html/multimedia-and-embedding/video-and-audio-content/multiple-audio-formats.html).)

This takes up less space than a video player, as there is no visual component — you just need to display controls to play the audio. Other differences from HTML video are as follows:

- The {{htmlelement("audio")}} element doesn't support the `width`/`height` attributes — again, there is no visual component, so there is nothing to assign a width or height to.
- It also doesn't support the `poster` attribute — again, no visual component.

Other than this, `<audio>` supports all the same features as `<video>` — review the above sections for more information about them.

## Displaying video text tracks

Now we'll discuss a slightly more advanced concept that is really useful to know about. Many people can't or don't want to hear the audio/video content they find on the Web, at least at certain times. For example:

- Many people have auditory impairments (such as being hard of hearing or deaf) so can't hear the audio clearly if at all.
- Others may not be able to hear the audio because they are in noisy environments (like a crowded bar when a sports game is being shown).
- Similarly, in environments where having the audio playing would be a distraction or disruption (such as in a library or when a partner is trying to sleep), having captions can be very useful.
- People who don't speak the language of the video might want a text transcript or even translation to help them understand the media content.

Wouldn't it be nice to be able to provide these people with a transcript of the words being spoken in the audio/video? Well, thanks to HTML video, you can. To do so we use the [WebVTT](/en-US/docs/Web/API/WebVTT_API) file format and the {{htmlelement("track")}} element.

> [!NOTE]
> "Transcribe" means "to write down spoken words as text." The resulting text is a "transcript."

WebVTT is a format for writing text files containing multiple strings of text along with metadata such as the time in the video at which each text string should be displayed, and even limited styling/positioning information. These text strings are called **cues**, and there are several kinds of cues which are used for different purposes. The most common cues are:

- subtitles
  - : Translations of foreign material, for people who don't understand the words spoken in the audio.
- captions
  - : Synchronized transcriptions of dialog or descriptions of significant sounds, to let people who can't hear the audio understand what is going on.
- timed descriptions
  - : Text which should be spoken by the media player in order to describe important visuals to blind or otherwise visually impaired users.

A typical WebVTT file will look something like this:

```plain
WEBVTT

1
00:00:22.230 --> 00:00:24.606
This is the first subtitle.

2
00:00:30.739 --> 00:00:34.074
This is the second.

…
```

To get this displayed along with the HTML media playback, you need to:

1. Save it as a `.vtt` file somewhere the server can serve (see below), such as in the same directory as the HTML file.
2. Link to the `.vtt` file with the {{htmlelement("track")}} element. `<track>` should be placed within `<audio>` or `<video>`, but after all `<source>` elements. Use the [`kind`](/en-US/docs/Web/HTML/Reference/Elements/track#kind) attribute to specify whether the cues are `subtitles`, `captions`, or `descriptions`. Further, use [`srclang`](/en-US/docs/Web/HTML/Reference/Elements/track#srclang) to tell the browser what language you have written the subtitles in. Finally, add [`label`](/en-US/docs/Web/HTML/Reference/Elements/track#label) to help readers identify the language they are searching for.

Here's an example:

```html
<video controls>
  <source src="example.mp4" type="video/mp4" />
  <source src="example.webm" type="video/webm" />
  <track kind="subtitles" src="subtitles_es.vtt" srclang="es" label="Spanish" />
</video>
```

In order to try this you need to host the files on a [local HTTP server](/en-US/docs/Learn_web_development/Howto/Tools_and_setup/set_up_a_local_testing_server). In the output in browser, you'll see a video that has subtitles displayed, kind of like this:

![Video player with stand controls such as play, stop, volume, and captions on and off. The video playing shows a scene of a man holding a spear-like weapon, and a caption reads "Esta hoja tiene pasado oscuro."](video-player-with-captions.png)

For more details, including on how to add labels please read [Adding captions and subtitles to HTML video](/en-US/docs/Web/Media/Guides/Audio_and_video_delivery/Adding_captions_and_subtitles_to_HTML5_video). You can [find the example](https://iandevlin.github.io/mdn/video-player-with-captions/) that goes along with this article on GitHub, written by Ian Devlin (see the [source code](https://github.com/iandevlin/iandevlin.github.io/tree/master/mdn/video-player-with-captions) too.) This example uses some JavaScript to allow users to choose between different subtitles. Note that to turn the subtitles on, you need to press the "CC" button and select an option — English, Deutsch, or Español.

> [!NOTE]
> Text tracks also help you with {{glossary("SEO")}}, since search engines especially thrive on text. Text tracks even allow search engines to link directly to a spot partway through the video.

## Embedding your own audio and video

For this task, why not go out into the world and record some of your own video and audio? If you have a phone, use that to record audio and video, transfer it to your computer, and try it out. You may have to do some conversion to end up with a WebM and MP4 in the case of video, and an MP3 and Ogg in the case of audio, but there are enough programs and tools out there to allow you to do this without too much trouble, such as [CloudConvert](https://cloudconvert.com/mp4-converter) (online) and [Audacity](https://sourceforge.net/projects/audacity/) (desktop application). We'd like you to have a go!

> [!NOTE]
> If you are unable to source any video or audio, then you can feel free to use our [sample audio and video files](https://github.com/mdn/learning-area/tree/main/html/multimedia-and-embedding/video-and-audio-content) to carry out this exercise.

We would like you to:

1. Save your audio and video files in a new directory on your computer.
2. Create a new HTML file in the same directory, called `index.html`, based on our [getting started template](https://github.com/mdn/learning-area/blob/main/html/introduction-to-html/getting-started/index.html).
3. Add {{HTMLElement("audio")}} and {{HTMLElement("video")}} elements to the page; make them display the default browser controls.
4. Give both of them {{HTMLElement("source")}} elements so that browsers will find the audio format they support best and load it. These should include [`type`](/en-US/docs/Web/HTML/Reference/Elements/source#type) attributes.
5. Give both of them a fallback `<p>` element inside the tags that provides a direct link to the media for non-supporting browsers.
6. Give the `<video>` element a poster that will be displayed before the video starts to be played. Have fun creating your own poster graphic.

<details>
<summary>Click here to show the solution</summary>

Your finished HTML should look something like this:

```html
<video controls poster="poster.png">
  <source src="rabbit320.mp4" type="video/mp4" />
  <source src="rabbit320.webm" type="video/webm" />
  <p>
    Your browser doesn't support HTML video. Here is a
    <a href="rabbit320.mp4">link to the video</a> instead.
  </p>
</video>

<audio controls>
  <source src="viper.mp3" type="audio/mp3" />
  <source src="viper.ogg" type="audio/ogg" />
  <p>
    Your browser doesn't support HTML audio. Here is a
    <a href="viper.mp3">link to the audio</a> instead.
  </p>
</audio>
```

</details>

## Test your skills!

You've reached the end of this article, but can you remember the most important information? You can find some further tests to verify that you've retained this information before you move on — see [Test your skills: Audio and video](/en-US/docs/Learn_web_development/Core/Structuring_content/Test_your_skills/Audio_and_video).

## Summary

And that's a wrap — we hope you had fun playing with video and audio in web pages! Next up, we'll present you with a challenge to test your skills with HTML media.

{{PreviousMenuNext("Learn_web_development/Core/Structuring_content/HTML_images", "Learn_web_development/Core/Structuring_content/Mozilla_splash_page", "Learn_web_development/Core/Structuring_content")}}
