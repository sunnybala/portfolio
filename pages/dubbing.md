## AI Speech Synthesis for Dubbing Terrace House 

**Quick Look:** Neural networks have been shown as being effective for cloning voices given speech data (ex. creating fake speeches by politicians). Recent multi-speaker networks work in the space of vocal characteristics and therefore no longer require training for each speaker individually. Here, I applied one such network to automatically dub an episode of a Japanese reality show (Terrace House) into English.

### Description 
Over the last few years a bunch of my friends kept recommending this Japanese reality show called Terrace House. Now, I like reality TV shows but I tend to watch them in the background while I do other activities. The biggest reason I kept passing up on watching this show was the need to constantly read subtitles. Look away and I’d have no clue what I missed.

I like reading, but let’s talk about how much reading is really involved in this kind of show. There’s 46 30-minute episodes, or 23 hours of footage. The average person reads at a rate of 200-300 words per minute (call it 250) and the average book is around 75k words, depending on genre. That’s 5 hours per book. If the average person is reading for 23 hours they could crush 4.5 books or 2/3 of Tolstoy’s 600k word War and Peace. 

#### Plan A - Screenreaders
My first thought was screenreading technology. Screenreading has been around for a while and it’ll just read on-screen text to you which is useful for accessibility purposes. I installed a chrome extension and got to watching but immediately hit a problem – every line is read with that same robot voice. My whole thing is that I don’t want have to look at the screen constantly. But if everyone’s got the same voice, there’s no way to tell who is talking so I ruled this out. 

#### Plan B – AI
People have been using neural networks to do voice cloning for a while now. Usually, you’ll take a bunch of hours of someone’s speech, then train the network to output more speech that mimics that person. That’s part of why some of the first voices to get cloned were politicians – their speeches are perfect training data. Now back in 2018, some researchers from google published <a href="https://arxiv.org/pdf/1806.04558.pdf"> this paper </a> demonstrating that instead of hours, they could do it with just a few seconds of a person’s voice. Which is nuts. 

Voice cloning at first seeemed nefarious and in the early results I saw, I was unsure about what good uses it could be put to. Well we can actually use this to clone every person’s Japanese voice, then have the cloned voices speak English. This is great because it means everyone gets a unique voice. Traditional voice cloning models are trained on pairs of text (input) + and the sound (output). The network needs to learn which letter make which sounds so that it can take any word that it hasn’t seen before and produce the sound for it. 

In this paper, they want to handle lots of people’s voices. Instead of just passing in some input text, you pass in the text + some information about who is speaking. This information is represented by a vector of numbers that correspond to different information about speech, like how high or low it is, or whether you have some kind of accent, and so on. This network can just take any text, and any speaker info, and produce speech. The cloning works by taking a speaker that the network hasn’t seen yet and condensing their voice down to whatever the characteristic numbers are. Mine might look like this. Morgan freeman’s might look like this. It can then these characteristics numbers (aka embeddings) + the text and generate a representation of the audio called a mel spectrogram. Finally, another network called WaveNet is used to take this mel spectrogram and convert it into audio you can actually listen to.

#### Voice Identification

So now I’ve just got to figure out how to get everyone’s voices. The good news is that the subtitles in shows and movies are stored in a really nice format that gives you start time, end time, and text. Unfortunately for this show they don’t say who’s speaking. So here’s where that embedding or characteristics comes back to us. Every piece of speech can be condensed into a set of numbers. I can then look at how different each piece of speech is from every other piece. This is a distance metric – I want voices that sound similar to be close together. Clustering algorithms can identify this for us. 

Now in this first episode there’s 6 panelists and 6 main characters. I know there should be at least 12 clusters right off the bat. Even in the course of a normal conversation people often make many different voices, especially when joking or reacting, so I threw in a few extras clusters in there. I figured I would just take one snippet of audio from each cluster and us that to generate all the audio.

As usual though there’s some complications. One reason this is so popular to do with speeches is that you get long stretches of isolated speech. When you have a tv show with multiple characters and group dynamics, this speech generation is going to struggle with situations where multiple people are speaking at the same time. I experimented with grabbing different audio clips from the clusters, and combining them, but the results were mixed sounded garbled. I ended up using an trick here -- I have the training data that the network was based off of. These are clean snippets of single speaker speech. So I just mapped each speaker cluster to the closest speaker from my training set. 

<img src="images/th-mel.png?raw=true"/>

In the image above I show the intermediate output for a single line of speech. On the top, we can see the cluster that this particular line has been identified as belonginging to. All other highlighted dots of the same color use the same vector of embeddings to produce speech. On the bottom is the mel spectrogram. While this format is not as useful by itself, it is important when diagnosing issues of audio quality. For example, certain sounds may not be replicated appropriately or the neural network output may have gaps. These sorts of issues were generally fixed by using the "clean" samples I mentioned earlier. 

Here's the result on the first 5 minutes of the first episode. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/9lKoGX6MbVI" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>