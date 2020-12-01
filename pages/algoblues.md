## Spherical Cucumber

**Quick Look:** I had recently learned about markov chains in my probability coursework and looked at applying it to generate blues improvisations over chord structures. By reading in a few pages of source material, I was able to build a transition matrix between notes and durations that was appropriate for the key signature. The end result was a piano melody that noodled around while drawing some common themes from the original source.  

### Description

In the simplest sense, a markov chain transition matrix represents the probability of transitioning from one state to the next. There will be one row and column for each state that is represented. Consider a simple piece of music where the notes are ABC, ABC, ACB. Here, there is a 2/3 chance that after A we see a B, and a 1/3 chance that we see a C. Extending this to an actual musical piece, there's another dimension that we care about: note length. In that case, each state represents a tuple of note length and pitch.

The trick to make this easy was to use the lilypond python library. This provides a syntax for writing out music like so. Each "word" in the syntax below corresponds to a pitch-length tuple. Therefore the markov chain just needed to randomly generate new valid words in this syntax and I would be left with a playable piece! 


 One output of the work can be listened to here:

<audio controls>
  <source src="https://sunnybala.com/portfolio/files/algoblues.mp3" type="audio/mpeg">
</audio>