# Green Screen

<img src="assets/images/video-tools/green-screen/banner.png" alt="Banner image of Green Screen">

?> Click [here](https://www.youtube.com/watch?v=-2UBoklCtjk&feature=youtu.be) for a video walk-through of Green Screen.

## What is Green Screen? 

The Green Screen tool allows you to cut out objects from videos, a process
known as rotoscoping. This common task is the bread-and-butter of video
manipulation. Once you have cut an object out of your video, you can swap the
background, display text behind it, or even selectively apply visual effects to
the region.

<img src="assets/images/video-tools/green-screen/composite.gif" alt="Sample motion graphics ouptut">

Most tools for rotoscoping require painstaking frame-by-frame edits by manually
highlighting the border of objects. With Runway, you can create professional
masks and cut object from videos with **just a ffew clicks**. Here are the
steps to get started...

## Step 1: Choose your clip

Open Green Screen by clicking on **Video Tools** under the media sidebar. Now
select an asset by opening the **Assets** sidebar. All of your exports from
other Runway tools appear here. If you want to use an asset from your computer
or external software, you can simply drag and drop onto the interface to get
started.

<img src="assets/images/video-tools/green-screen/clip-selection.gif" alt="Gif opening the assets bar">

?> Our tool is designed to track individual objects throughout a scene. If you
have lots of footage to cut, it's best to trim into clips with relatively
consistent camera angles and lighting conditions, and then edit each one with
Green Screen individually. If you want to track two separate objects in the
same video, we recommend you use Green Screen twice to track them separately.

## Step 2: Click to create keyframes

To start off the process, seek to an initial frame which contains the desired
object in clear view. Then click on the object in frame to create your initial mask.

The toolbar above the timeline allows you to switch between
**Include** clicks which expand the mask to the clicked location and
**Exclude** clicks which retract the mask. You can also swap between
**Foreground** and **Background** to see what the masked object looks like.

Now that you have an initial mask, you can click **Preview** to see the
expected result if you were to propagate the mask to the rest of the video. You
can also click on the timeline or use the arrow keys to check the results on a
frame-by-frame basis.

<img src="assets/images/video-tools/green-screen/click-and-propagate.gif" alt="Gif clicking to generate initial mask and then propagating">

?> You'll notice that there are regions of video where masking can be improved.
The goal is to create a set of keyframes from which Green Screen can estimate
the mask for the whole video. A new keyframe is usually neded when the target
apperance changes (e.g. a body part appears for the first time, the subject
moves to a different background, or lighting conditions vary).

Now you rinse-and-repeat, creating keyframes where the current results are
lacking, and then previewing the updated results. Depending on the amount of
movement and background complexity, Green Screen may need just a pair of
keyframes for the entire clip, or it may require one keyframe every few 
seconds.

## Step 3: Export your result

Once you're satisfied with the mask, click **Export** to output a video file.
You can change the name of the video, and select a
[chroma-key](https://en.wikipedia.org/wiki/Chroma_key) background.

<img src="assets/images/video-tools/green-screen/export.gif" alt="Gif showing the export process">

The output will appear in your **Assets**, from which you can export the file
into other software to add visual effects.

## Bonus: Composite text with iMovie

Using our exported file in any video editor or compositor is quite easy. Here
we use iMovie, but similar effects can be achieved with most video software.

First, place the desired text on top of your source video. Then, import the
output from Green Screen into iMovie and place it on top of the desired text.
By applying a the green-screen effect, as shown
[here](https://support.apple.com/en-us/HT210891) you can overlay just the
subject on top of the text.

<img src="assets/images/video-tools/green-screen/compositing.gif" alt="Gif showing how to composite with iMovie">

Congratulations, you've just done your first Green Screen!

If you have any questions or feedback, [let us know](mailto:support@runwayml.com)!
We can't wait to see what you create.
