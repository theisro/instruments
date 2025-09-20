# SynthDefs and Synths

A SynthDef is like a recipe for a cake. How to bake a cake for a certain number of guests, how much egg and sugar to use etc. A Synth is the actual cake itself. An instance of the cake baked using the recipe (SynthDef)

# SynthDef - Simple Sine

```
(
SynthDef(\mysine , { |freq = 440, amp = 0.3 |
    var sig;
    sig = SinOsc.ar(freq, 0, amp);
    Out.ar(0, sig ! 2);
}).add; 
)

x = Synth(\mysine, [\freq, 220, \amp, 0.2]);

x.free;
```

## Code Explanation
The brackets (or paranthesis) denotes a block or region of code, which can be executed by keeping the cursor anywhere within the region and pressing Ctrl + Return . 

`SynthDef` begins the definition of the Synthesizer. `\mysine` denotes the name of the Synthesizer Definition,
the recipe if you will. From the opening curly brackets till the closing brackets {} we see the actual 
code of the Synthesizer Definition. The parts between the pipe symbols '|' denote the arguments to the SynthDef.
So `| freq = 440, amp = 0.3 |` indicates two named arguments to the SynthDef, called `freq` and `amp`. 

The line `var sig;` defines a variable called sig. In the next line `sig = SinOsc.ar(freq, 0, amp)` the variable
sig is being assigned a value of the Sine Oscillator and then in the next line `Out.ar(0, sig ! 2)` the signal
is being played. `0` indicates the channel to be played out to. The code `sig ! 2` means the value is repeated
twice as a parameter. So it provides the same signal for right and left channel. The `!` symbol means to repeat 
the value to the left of the symbol the number of times denoted to the right of the symbol.

To execute this code, place your cursor anywhere within the SynthDef block and press Ctrl + Enter.

Then place your cursor on the `x = Synth(\mysine...)` line and press Ctrl + Enter or Shift + Enter . You should 
hear a tone playing. Then you can move your cursor down to `x.free;` and press Shift + Enter again and it 
will stop. The parameters to the Synth are given as an array (an array is a list of elements). So 
`[\freq, 220, \amp, 0.2]` pairs up the values in the list and `freq` gets the value of `220` while `\amp` gets 
the value of `0.2`

# SynthDef - Note with Envelope
```
(
// A percussive synth
SynthDef(\beep, { |freq = 440, amp = 0.2, sustain = 0.5|
    var env = Env.perc(0.01, sustain, amp);   // attack, release, level
    var sig = SinOsc.ar(freq) * EnvGen.kr(env, doneAction: 2);
    Out.ar(0, sig ! 2);
}).add;
)

// Play notes (they stop automatically)
Synth(\beep, [\freq, 440]);
Synth(\beep, [\freq, 660, \sustain, 1]);

```

## Code Explanation
The code is almost the same as the previous Synth except it has an envelope. The envelope converts the tone 
into a note. So that it has Attack, and Release. Remember that envelopes can have Attack, Decay, Sustain and 
Release, but don't necessarily need to have all 4 parts. 

The envelope also has a parameter called `doneAction: 2` which tells SuperCollider that the note needs to be 
released after it is finished.
