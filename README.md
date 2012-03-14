# Bug: Audio playback in background tab / when Browser is not the current app is inconsistent.

## Desired behaviour
As occurs on **Chrome Desktop**: Clicking on the 'Go' button will set the tracks playing, looping forever

## Implementation details
**Note:** The implementation of this bug contains an example which has one <audio /> tag. Hitting 'Go' will set the sourc attribute of the <audio /> tag to point to the first track, and when the <audio /> tag can play the track, it begins playback. When this track ends, the source is updated to point to a new track, and playback begins again. After the third track, the first track is played again, ad infinitum.

The playback is implemented in this manner as this is the de facto standard for playlist behavior on iOS & Android Browser. However, Android Browser will not

## Observed behaviour
**Note:** the first inconsistency is seen in the way that playback begins: this is not the focus of this example. Android Browser happily begins playback when the user hits the 'Go' button. Android Chrome will not allow the 'audioPlayer.play()' action to be called from within the 'canplaythrough' event handler, so the user has to manually hit the 'play' button in the <audio /> controls. I believe this is intentional - the play() call can only happen in response to a direct user action, not a callback, to prevent abuse of the <audio /> tag. 

After playback has started