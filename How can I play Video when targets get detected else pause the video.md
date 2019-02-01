
# How can I play Video when targets get detected else pause the Video

It was asked on [AR tutorial series week 1](https://careerhigh.in/blog/20/) by Shubhendra Singh. If you havent checked out [AR tutorial series](https://careerhigh.in/blog/18/), go check it out.
#vuforia #AR #unity
<hr>
First untick the "Play on Awake" of your videoPlayer, Because of this, video starts playing when your apps starts.

Now we have to configure 
`DefaultTrackableEventHandler` 
(you will find it in inspector window of image target) file of your image target so that we control the Play or Pause your video according to our need,

Open it in visual studio(or any other editor)
Add following below `using UnityEngine`
```
using UnityEngine.Video;
```
And then take a video player variable inside the above mentioned class like below.
```
public VideoPlayer videoPlayer;
```
Now inside OnTrackableStateChanged configure it like this (It will get current component video):
```
videoPlayer = mTrackableBehaviour.GetComponentInChildren<VideoPlayer>();
```
For controlling Play or Pause your video you  have to add following snippet after above line:
```
if (newStatus == TrackableBehaviour.Status.DETECTED ||
  newStatus == TrackableBehaviour.Status.TRACKED ||
  newStatus == TrackableBehaviour.Status.EXTENDED_TRACKED)
{
  videoPlayer.Play();
  OnTrackingFound();
}
else
{
  videoPlayer.Pause();
  OnTrackingLost();
} 
```
Save it.
Now when you got inspector window of image target, you will see one new variable "Video Player" below `DefaultTrackableEventHandler`. Double click on it, and select "Quad"

Now you video will start playing when target get detected else the Video will be paused.
