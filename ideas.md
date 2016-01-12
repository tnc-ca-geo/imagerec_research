##First thoughts and Ideas##

*@postfalk*: After viewing the two example videos, I think there are three levels 
of complexity to address.

1. **Detecting activity**: My impression from the example videos is, that catching 
fish and on deck activity is highly correlated. Especially if the system also 
uses gear sensors which would make it easy to distinguish between fishing and 
e.g. activity during departure from or arrival at a harbor. Given the bright 
yellow closing and the relatively unchanged background that should be pretty **easy**.

2. **Detecting the animal captured**: This one seems to be tricker, especially if we 
try to detect the animal independently of the above mentioned activity which had 
to be filtered out. The contrast between the animal and the background seems 
rather low. However, we should look into this level of complexity before we 
would spend all the money on a problem that might turn out to be rather trivial.

3. **Species detection*:** This is probably where the real challenge lies and where 
we should spend our resources. However, in order to get here we need to present
a good training data set in order to not put the burden of a lot of grunt work
on the competing teams (in which case the price might be actually not that
high.)

###Goal###

A real-time algorithm that would create a data report from video stream.

@mmerrifield Do we have also a result example dataset/report to look at?

###Next steps to explore###

1. **Video training data sets**: I found a lot of image data sets for machine 
learning competitions, testing, and bench-marking but not too many video 
examples. I mentioned earlier that videos could be just treated as a pool of 
images. Technically that holds true. The problem might be that we would have 
an enormous amount of very similar images causing potentially over-fitting 
or not providing enough variance to make the resulting algorithm universally 
applicable.

###Designing the training data set is a challenge itself###

1. **Explore community standards**

2. **Design data structure to be fed in training algorithms**

3. **Implement workflow with vendors that generating the data:** 

    - this might require customization of software to turn reporting in 
    actual image/frame tags

4. **Discuss problems of releasing training data set**:

    - animal right activism

    - property of the company

    - others?


###Data Structure###

A training dataset would consist of a **video** (.mp4) file and an **annotation 
file** (e.g. [CMML](https://en.wikipedia.org/wiki/Continuous_Media_Markup_Language)&mdash;XML, 
very verbose, [Timed text](https://en.wikipedia.org/wiki/Timed_text)&mdash;very simply,
[TTML](https://en.wikipedia.org/wiki/Timed_Text_Markup_Language)). Most of these
standards were created for adding 
[subtitles](https://en.wikipedia.org/wiki/Category:Subtitle_file_formats) to movies. 
This seems to be very convenient since it allows to spot check the tagging in media
players as common as [VLC](http://www.videolan.org/index.html). 

However, before we create the dataset we have to figure out whether there are established
standards, best practices.

We talked about something like this:

```txt
frame, timestamp, tag
0, 0, None
1, 40000, None
...
420, 16800000, tuna
...
600, 24000000, tuna
601, 24040000, None

```

The time stamp is in &#181;s to accommodate slow motion. The frames are not necessarily
evenly spaced. However, that should not be a problem giving the speed of the processes
we are watching.

In Timed Text it would look like this (much more space saving):

```txt
00:00:00,000 --> 00:00:16,800
none

00:00:16,800 --> 00:00:24,000
tuna

00:00:24,000 --> ...
none
```
