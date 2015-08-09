#Next Steps
There are a few different ideas we have about where the video player needs to go, and how we'll best get it there. This page's purpose is to collect and document those ideas.

###HLS (Adaptive Streaming)
After doing some extensive R&D it's apparent that in its native form, HLS video will not be usable for interactive videos. This is due to varying levels of browser support, inconsistencies, etc. The main sticking points seem to be looping and seamlessly transitioning to new videos.  

###Possible Solutions:

>**THEOPlayer**  
<font size="3">The THEOPlayer team may be able to help solve the issues with HLS playback. If they are able to develop an HLS playback engine that can seamlessly loop, as well as seamlessly switch streams to another video (once a selection has been made), problem solved.</font>

  
> **HLS + Progressive (Hybrid)**  
<font size="3">We've had some discussions about whether we could use progressive videos just for looping and insert them at the end of HLS videos. This could work but might be problematic.</font>
