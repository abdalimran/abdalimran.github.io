---
layout: post
title: Extracting Audio from Video using Python
category: 
    - "Miscellaneous"
---

We'll start by installing `ffmpeg` and `moviepy` packages using the following pip command.

{% highlight python %}
pip install ffmpeg moviepy
{% endhighlight %}

**Next, we'll import MoviePy:**
{% highlight python %}
import moviepy.editor as mp
{% endhighlight %}

**Next, we'll load the Video Clip:**
{% highlight python %}
video_clip = mp.VideoFileClip(r"video_file.mp4")
{% endhighlight %}

MoviePy supports various video formats like:
* WMV (wmv, wma, asf*)
* OGG (ogg, oga, ogv, ogx)
* 3GP (3gp, 3gp2, 3g2, 3gpp, 3gpp2)
* MP4 (mp4, m4a, m4v, f4v, f4a, m4b, m4r, f4b, mov)

**Now, we'll extract the audio:**
{% highlight python %}
video_clip.audio.write_audiofile(r"audio_file.mp3")
{% endhighlight %}

Here, we can  choose different audio format as our preference. Some formats as listed below:
* MP3
* AAC
* WMA
* AC3 (Dolby Digital)
