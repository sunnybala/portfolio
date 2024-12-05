## VR Conducting Game

**Quick Look:** As an early adopter of the HTC Vive, I was amazed by the possibilities. For this project I learned how to use the Unity game engine and designed a game to conduct a virtual orchestra. I used MIDI files to get the scores across instruments then allowed the player to control the tempo, volume, and cue-ing individual instruments to come in.

### Technology Used
- Unity Game Engine (First Time)
- MIDI Files
- Python 

### Description

I always loved rhythm based games growing up. While I never owned Dance Dance Revolution or Guitar Hero, I spent countless hours playing them at friends' homes. I was interested in seeing if I could make a game that was the equivalent in an orchestral setting. The ability to track hand motions in VR meant that actions like pointing at a specific orchestra section to start it seemed possible. 

For the music here I fell back to MIDI files. The whole score of musical pieces is embedded in these files which makes them great for taking apart. I selected a fugue with 3 players that enter one after another. Since each track is separable, I was able to mute individual players. This is what creates the cue-ing behavior -- if you fail to point and click the instrument when it is that instrument's turn to begin, that track will simply be missing in the audio output. 

In this initial prototype I also added tempo and volume. The tempo is determined by counting the time between strikes of two plates in the air with the baton. These plates are only fully opaque for debugging purposes. The amplitude of the conducting can be calculated using distance from the bottom plate as well, allowing the output volume to vary. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/ECIkdqrps7M" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>