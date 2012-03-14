# HTML5 audio test
This simple test case is intended to show some odd behaviour in the handling of javascript events pertaining to the HTML5 audio tag in mobile browsers, specifically around the handling of events in background tabs, or while another application is active.

## Desired behaviour
The test contains 3 mp3s. Upon clicking 'Go', the src attribute of the audio tag will be changed to point to track one. When the 'canplaythrough' event is fired, the track will automatically start playing. When the 'ended' event is fire, the src attribute will be updated to track 2, and the process will repeat. On completion of track 3, it should loop around to track one.

## Unintended differences between browsers
Safari (OSX): this should work without issues
Chrome (OSX): this should work without issues
Firefox (OSX): this should work without issues
Chrome (Android): playback cannot be started in the callback of the 'canplaythrough' event. User will need to manually hit the 'play' button in the audio controls, every time the track changes.
Browser (Android): playback cannot be started in the callback of the 'canplaythrough' event. User will need to manually hit the 'play' button in the audio controls, for the first track only.
Safari (iOS): playback cannot be started in the callback of the 'canplaythrough' event. User will need to manually hit the 'play' button in the audio controls, for the first track only.

## Observed behaviour
Android Browser: Start playback, switch out of the application / lock your phone's screen. The audio will continue to play, but at the end of the track it will not advance to the next track. Switching back to it will cause the canplaythrough event to trigger the next track.
Android Chrome: Start playback, switch out of the application / to another tab. The audio will stop immediately. 
