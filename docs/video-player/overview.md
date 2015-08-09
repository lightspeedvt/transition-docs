#Video Player
 In order to "stay ahead of the game" we've always developed custom playback solutions instead of using 3rd party players.  Our current solution is based in Flash with a trimmed-down mobile version, but due to browser advancements and ongoing politics (browsers shipping without Flash, etc) it's time to consider other options.

***

###Latest Advancements
We've recently created a new [Knockout-Based Component](https://github.com/lightspeedvt/video-player) that leverages [MediaElementJS](http://mediaelementjs.com) behind the scenes. This allows us to support things like HLS video on the desktop (via Flash) and also provides a single ui for both desktop and mobile. The component is currently being used for the course previews inside Blue-Steel.

This solution works fairly well for single (non-interactive) videos but has serious limitations moving forward, namely:

- **Uses Flash (on Desktop)**  
Browsers are quickly dumping Flash support or turning it off by default
- **Relies on native HLS support on mobile**  
iOS has this pretty well handled but even the latest versions of Android still<br>have significant issues.
- **Need to implement custom ui features**  
Captions, bandwidth selection, etc are standard features in most 3rd party players but will require a bit of custom dev to get working in our player. It's not prohibitive, but will take some time.

***

###The Path Forward
We've had a good run with in-house development, however the time is now to start thinking about 3rd party solutions.  

The technology that is the most promising seems to be [THEOplayer](https://www.theoplayer.com/) which uses a custom decoding solution in JavaScript. Due to the fact that their code has low-level access to playback mechansims we should be able to contract them to customize a solution for LightSpeed VT.

We've had some dialog with [Pieter-Jan Speelmans](mailto:pieter-jan.speelmans@opentelly.com) at OpenTelly who has been very helpful, interested and seems willing to accomodate our needs.  

Check out the [Next Steps](next-steps) page for more information.

***

###Video Player - Existing Features
There are a number of features from our current Flash player that would need to be replicated and supported in a new playback solution:

>**Captions**  
<font size="3">We currently have a large number of caption files in dfxp format, these files are hosted on Cloudfront along with the video files. Most have multiple languages, one file per language.  Any player we develop should be able to load these files and display captions accordingly.</font>

>**Interactivity**  
<font size="3">Our current interactive solution relies on custom "manifests" that are written in JSON format and hosted on Cloudfront. The player loads these files and tailors the user's experience based on their interactions, while also providing basic reporting. For a detailed explanation, please [see the "Interactivity" page.](interactivity)</font>

>**Skip Prevention**  
<font size="3">Depending on the user's access level within the system, the player will prevent forward seeking in order to force the user to wwtch the video for its complete duration.</font>


###Video Player - Desired Features
Based on user feedback and desire to expand our product offering, there are a number of new developments we'd like to see with the video player.

>**Adaptive Streaming**  
<font size="3">We currently serve most of our video content as progressive download. We would like to provide an adaptive streaming solution for users on varying bandwidth.</font>

>**Resume or Seek To/From any Point**  
<font size="3">Ideally the player could start from any time, it would be even nicer to support range requests to show clips as well as the full video.</font>

>**Content Protection**  
<font size="3">We've had a few occurances of video theft and customer inquisitions about protecting video content.</font>

>**Enhanced Interactivity / API**  
<font size="3">Add more capabilities to the interactive hotspots, add to cart, etc</font>

>**Portability**  
<font size="3">Ideally the player would be embeddable either via an iframe or javascript solution so that it can be used outside of the Training Center.</font>
