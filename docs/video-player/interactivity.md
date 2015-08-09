#Interactive Playback
Interactive video playback is a crucial part of what sets the LightSpeed VT platform apart from other training systems. This document will provide an overview on the concepts and details that go into our interactive playback.

***

###Example Sequence
The following diagram presents a typical interactive scenario. You'll notice a few things:

- **Videos can have loop points/sections**  
Typically when there is a prompt/interaction, the video will loop until the user makes a selection. There will be a defined loop time which the video will return upon completion. It will remain playing, indefinitely.

- **User-interactions can control the "path" of the playback**  
In the diagram below, once the user entered the loop portion of the "Intro Video", there would have been two options presented to the user. Each selection would continue playback but with a different video.

- **Videos can link to another video upon ending**  
Video A doesn't have any options so it simply procedes to the End Video once it completes.

- **Videos can link to themselves**  
Video B would have a selection that will cause the video to replay.


<br><br>
```text
                             +-----------+                  
                             |           |                  
                             |  Video A  |                   
                             |           |                   
+---------------+------+---> +-----------+----------> +-------------+
|               |      |                              |             |
|  Intro Video  | Loop |                              |  End Video  |
|               |      |                              |             |
+---------------+------+---> +-----------+------+---> +-------------+
                             |           |      |                    
                             |  Video B  | Loop |                    
                             |           |      |                    
                         +-> +-----------+------+---+                
                         |                          |                
                         |                          |                
                         +--------------------------+                
```
***
###JSON Manifest Examples
The JSON manifest format consists of a list of video objects, each with their own properties. In this section, we'll outline what the configuration options look like and document their functionality.

> **Video Object**  
<font size="3">Videos are indexed by an id, in this case it's using `"intro"` which is special.<br>The player will always start with the `"intro"` video first.</font>

```json
{
    "videos": {
        "intro": {
            "question": "When it comes to strategizing you should...",
            "buttons": [],
            "loopStart": [0, 50],
            "src": "video.mp4",
            "captions": {
                "Spanish": "spanish.dfxp.xml",
                "English": "english.dfxp.xml"
            },
            "next": "intro",
            "ending": {
                "video": "intro",
                "url": ["http://www.google.com", "_blank"],
                "complete": false
            }
        }
    }
}
```

|Property|Description|
|----|----|
|`question`|Plain text representation of the prompt/question used in the video|
|`buttons`|Array of button objects|
|`loopStart`|Array of minutes, seconds values that tell the player where to loop to once the video ends|
|`src`|URL of the video resource|
|`captions`|URLs of caption files indexed by language|
|`next`|Play another video based on id specified, deprecated version of the `ending` object|
|`ending`|This object instructs the player what to do upon completion. The available properties are:<ul><li>`video` - Play another video based on id specified</li><li>`url` - The player will open a link based on the `[href, target]` properties specified</li><li>`complete` - Controls whether the video is completed via javascript. Useful for some instances where external resources need to be loaded before proceeding.</li></ul>
|

> **Button Object**  
<font size="3">The following example shows a video with a single button</font>

```json
{
    "videos": {
        "intro": {
            "buttons": [{
                "img": "twitter-button.png",
                "width": 100,
                "height": 50,
                "x": 100,
                "y": 300,
                "label": "Complete w/ B",
                "action": "complete",
                "value": "B",
                "time": [0, 18],
                "video": "intro",
                "url": {
                    "href": "http://videos.lightspeedvt.com/file.pdf",
                    "target": "_blank",
                    "specs": "width=550,height=440"
                }
            }]
        }
    }
}
```

|Property|Description|
|----|----|
|`img`|Url for an image to load instead of a hotspot|
|`width`|Pixel value for the button area's width|
|`height`|Pixel value for the button area's height|
|`x`|Pixel value for the button area's left position|
|`y`|Pixel value for the button area's top position|
|`label`|Text to show when debug is set to true|
|`action`|A string value that is sent to any selection callbacks along with the value property|
|`value`|A string value that is sent to any selection callbacks along with the action property|
|`time`|An array in the format of `[mins,secs]` that tells the player when to activate the button area|
|`video`|The id of a video to play once clicked|
|`url`|An object with the following properties:<ul><li>`href` - the url to be opened</li><li>`target` - the window in which to open the url</li><li>`specs` -properties for popup window</li></ul>|
