## AlgoBlues

**Quick Look:** I had recently learned about markov chains in my probability coursework and looked at applying it to generate blues improvisations over chord structures. By reading in a few pages of source material, I was able to build a transition matrix between notes and durations that was appropriate for the key signature. The end result was a piano melody that noodled around while drawing some common themes from the original source.  

### Description

In the simplest sense, a markov chain transition matrix represents the probability of transitioning from one state to the next. There will be one row and column for each state that is represented. Consider a simple piece of music where the notes are ABC, ABC, ACB. Here, there is a 2/3 chance that after A we see a B, and a 1/3 chance that we see a C. Extending this to an actual musical piece, there's another dimension that we care about: note length. In that case, each state represents a tuple of note length and pitch.

The trick to make this easy was to use the lilypond python library. This provides a syntax for writing out music like so. Each "word" in the syntax below corresponds to a pitch-length tuple. Therefore the markov chain just needed to randomly generate new valid words in this syntax and I would be left with a playable piece! 

Example Lilypond syntax that encodes both pitch and note length:
```
 r2 r4 r2 g''4 des''8 c''4 g'8 bes'8 
 r4 bes'4 r2 r4 r2  r8-end g'8 bes'8 
 c''8 bes'8 des''8 c''8 bes'8 des''8 
 c''8 bes'8 des''8 c''8 bes'8 g'8 c''8  
 r8-end bes''4 r8 g''4 des''8 c''4 g'8
```

 Each chord had it's own markov chain. Finally, there was one "finisher" matrix corresponding to the ending of the pieces in the training set. This helped the ending of the piece have some cohesion. One output of the work can be listened to here:

<audio controls>
  <source src="https://sunnybala.com/portfolio/files/algoblues.mp3" type="audio/mpeg">
</audio>

The code is available at my <a href="https://github.com/sunnybala/AlgoBlues">github</a>.