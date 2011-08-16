AudioStream
============

Installation
------------

This plugin allows you to use [Matt Gallagher's AudioStreamer classes](https://github.com/mattgallagher/AudioStreamer "Cocoa with Love does it again!") in your iPhone PhoneGap app.

Add the plugin much like any other:

1.      Add the AudioStream.m, AudioStream.h, AudioStreamer.h and AudioStreamer.m classes to your Plugins folder in Xcode
2.      Add the AudioStream.js file to your www folder
3.		Add the AudioStream.js to your html file. eg: `<script type="text/javascript" charset="utf-8" src="AudioStream.js"></script>`
4.      Add the plugin to the PhoneGap.plist
5.      Here is where it differs slightly, [add the CFNetwork.framework to your project in Xcode](http://paikialog.wordpress.com/2011/03/09/xcode-4how-to-add-framework-into-project/ "Xcode 4–How to add Framework into project?").

### Example
```javascript
// Don't use these functions "as is", they're terrible. They just show the methods available.
// You should be doing something useful with the progress and the changes in state at the least.
function onDeviceReady()
{
	audioStreamer = window.plugins.audioStream;
	audioStreamer.setStreamType("mp3"); // only needed if your stream's type isn't auto-detected
}
function play(urlToStream)
{
	audioStreamer.play(urlToStream,playbackStateChanged,onError);
	navigator.notification.activityStart();
}
function stop()
{
	audioStreamer.stop(playbackStateChanged,onError);
}
function playbackStateChanged(state)
{
	console.log("state: "+state);
	switch (state) {
		case "isPlaying":
			navigator.notification.activityStop();
			progressTimer = setInterval("console.log(audioStreamer.progress + ' seconds')",300);
			break;
		case "isStopped":
			navigator.notification.activityStop();
			clearInterval(progressTimer);
			break;
		case "isWaiting":
			navigator.notification.activityStart(); 
			break;
		default:
		
}
function onError(error) {
	console.log(e.message);
}
```


## License

The MIT License

Copyright (c) 2011 Tommy-Carlos Williams (github.com/devgeeks)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
