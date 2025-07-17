# Sub-Oscillator-Module
DIY sub oscillator module for eurorack synthesizers.

# Intro
Adding a sub-oscillator is a simple way to give a main oscillator some due bottom end.

A sub oscillator is an oscillator which frequency is one or two octaves lower than the oscillator it is paired with.

Honorable synthesizers using sub-oscilaltors to beef their voice/s include the Roland Juno 106, SH101, the Korg Polysix and many other. 

This module, in particlular, takes inspiration from the SH101 sub-oscillator generation section, but with additional features.

# Sub-Osc Circuits

This sub-oscillator module produce two distinct waveforms, square and triangle, processed starting from the main wave at it's input.

At module's output we have a mixed wave made of the internally generated sub-oscillator and the original wave.

In the following a detailed description of the whole circuit stages.

**First Stage**

The square wave is generated directly from the incoming main oscillator waveform. Since this is a standalone module, meant to be compatible with all sort of environments (or at least the most part of them), I had to take into consideration that the incoming wave could be AC-coupled (Eurorack systems standard), or DC-coupled.

To account for this, a DC offset circuit is placed at the very first stage of the design.

A "doubling" stage follows, where the incoming wave is (a) sent to the final mixing stage (or to the blend stage), (b) buffered and sent to the sub-oscillator generation section.

**Squarewave Sub-Oscillator Generation**

The sub oscillator generation section is in charge to turn a "copy" of the incoming wave into a square wave.

An opamp in Schmitt Trigger configuration comes first, "squareing" the original waveform for further processing.

The opamp in this configuration outputs a square wave with "maxed" amplitude (+/- the power supply voltage) and threshold voltage given by the values of surrounding resistors.

The trigger is dimensioned such to have threshold voltages of +/-1V circa. This makes it possible to generate the square wave even starting from low amplitude incoming waves. To have further room for "weak" signals/waves, the wave "copy" hitting the sub-osc generation circuit arrives already amplified from the "buffering" stage.

Out of the trigger circuit we then have a square wave with the same frequency as the original wave and max amplitude (+/-12V in eurorack systems).

Nex step is to half the frequency to lowen the square wave pitch of at least one octave. The frequency is divided by using the square wave as clock source for a D flip flop integrated circuit (CD4013), a well known approach (Roland adopted such in the SH101 synthesizer).

At each rising edge of the clock, the flip flop outputs a HIGH or LOW signal at the same voltage it is powered with, thus generating a square wave with half the clock frequency (one octave lower, it is).
By placing more D flip flops in series we can further divide the frequency of the clocking square wave.

Two flip-flops are housed in a single CD4013 IC, making it straightforward to design a two-stage frequency divider.

A nice thing about D flip-flops is that, even if commonly used in digital circuits, they tollerate a "high" incoming voltage with no problems, but no AC-coupled clock signals. A rectifying diode is then included to ensure proper operation.

The signal at flip-flop output has the same amplitude of the voltage juicing it, so we end with a lower frequency, DC biased, 0/+12V square wave.

Although the human ear cannot distinguish between AC or DC-coupled audio signals, offsets become significant when summing multiple signals. For this reason, an AC offset circuit completes the sub oscillator generation circuit.

**Square-to-Triangle Converter**

The module gives the choice between square or triangle wave sub oscillator.

The square wave generated in previous stage is converted to triangle with an op-amp in integrator configuration. This is a well known op-amp configuration, even if not encountered that much in DIY synth circuits.

**Final Stage**

As a final step, we want to mix the incoming waveform and the internally generated sub-oscillator.

Before hitting the mixing stage, the sub-oscillator level can be attenuated by a potentiometer in voltage divider configuration. This is the configuration of the "sub level" front board.

I also liked the idea of a blend control over direct wave and sub osc level, instead of the control over sub level only, then designed a second PCB version.

The blend control is made through a potentiometer linking the two waves before the final mixer section. The amount of attenuation of one wave with respect to the other is determined by the fraction of signal grounded by the potentiometer.g sub-oscilaltors to beef their voice/s include the Roland Juno 106, SH101, the Korg Polysix and many other.

# Features

The module has all the features one could expect from such a device.

User can set the relative amount of direct and sub-waves, or the sub level only, simply by turning a knob placed in the upper part of the panel.

The module has a switch to remove DC coupling in case the master wave is in the positive domain of voltages. DC coupling is not up to eurorack standard, but there are actually a lot of out-of spec modules out there, especially in the do-it-yourself realm, and I wanted something working in "any" environment.

User can select the sub-oscillator waveform between square or triangle through a SPDT switch, readily accessible from the front.

Another feature is the possibility to set the trigger level of the Schmitt Trigger. The circuit is dimensioned such that even attenuated main waves can trigger the square wave generation, but if your output is dirty and the main wave hot enougth, increasing the trigger level could fix some erratic behaviour, especially with complex waveforms.

The trigger level control is accessible from the back of the module.

Module calls for +/-12V, but should work even with +/-15V.

# Acknowledgments

Many thanks goes to the nice girls and guys at [JLCPCB](https://jlcpcb.com/IAT) for sponsoring PCBs manufacturing for this module.

Without their contribution this project would have never reached the current level of development, like many others projects of mine now.

In this run they also sponsored the production of a rev.2 of the [CV mixer](https://www.instructables.com/4-Channels-AudioCV-Mixers-for-Eurorack-Synthesizer/) panel board, the original having a minor offset issue in the design. This made it possible to check the new design and share a now perfectly fitting panel board.

JLCPCB is a high-tech manufacturer specialized in the production of high-reliable and cost-effective PCBs. They offer a flexible PCB assembly service with a huge library of more than 600.000 components in stock at today.

3D printing is part of their portfolio of services so one could create a full finished product, all in one place!

What about nano-coated stencils for your SMD projects? You can take advantage of a coupon and test it for free in these days.

By registering at JLCPCB site via [THIS LINK](https://jlcpcb.com/IAT) (affiliated link) you will receive a series of coupons for your orders. Registering costs nothing, so it could be the right opportunity to give their service a due try ;)

My projects are free and for everybody. You are anyway welcome if you want to donate some change to help me cover components costs and push the development of new projects (I have a new one on a arpeggiator module I would really like to realize and share...)

[>>HERE<<](https://paypal.me/barito77) is my paypal donation page, just in case ;)




