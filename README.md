Pd patches for controlling a guitar synthesizer live rig
========================================================

These are [Pd](https://puredata.info/) patches that I use to control a combination of
guitar synthesizers and amplifiers for a performance live rig I use. This configuration
is obviously tailored towards my equipment and needs, but I'm publishing it as _potentially_
to be of benefit to others wanting to use Pd to "tame" their configuration of gear. I
obviously make no claim on the usefulness, or benefit for anyone else. It's also offered
for free, with a MIT license, so that is a statement of it's potential value, too...

The application is that I have two guitar synthesizers
(an [Axon AX-100MKII](https://www.soundonsound.com/reviews/terratec-axon-ax100-mkii), 
and a [Boss SY-1000](https://www.boss.info/us/products/sy-1000/)) that are connected to a
[Primova GX-2 GK-13 switcher](https://www.primovasound.com/products/gx2/index.php/). 
I use a number of older Roland 24 pin guitars, such as the
[Roland G-202](http://www.gr300.com/G-202.html), 
[G-707](http://www.gr300.com/G-707.html),
[G-808](http://www.gr300.com/G-808.html), 
[Ibanez IMG-2010](http://www.gr300.com/img2010.htm) 
models, via a [Wayne Joness BX-13-VC 24 pin to GK-13 adapter](http://www.gr300.com/BX13.htm).
Each guitar has differing hexaphonic pickup levels which the Primova GX-2 can be set to adjust gains
for, and each synthesizer is configured for best tracking on both of the synths. In
addition, I run a Tama classical guitar equipped with [RMC](https://www.rmcpickup.com/)
hexaphonic piezo pickups into the GX-2 that can control the synthesizers, as well as the
magnetic pickup guitars.

The problem to be solved is that all three devices need to be changed if a guitar is
changed. The Primova GX-2 actually performs some of that function, but has no support for
the Axon AX-100. The solution was to produce a set of Pd patches which allows sending
[System Exclusive (SysEx) MIDI](https://midi.org/midi-1-0) messages to both synths to
change to the guitar settings which have been preprogrammed for each guitar, and to send a
patch change to the GX-2 to select it's patch that is configured for that guitar. This is
the patch `Guitar_switcher.pd`.

Additionally, I run the "normal" (mono pickups) guitar of the SY-1000 "sub" output into
two valve ("tube") amplifiers, which both have footswitched channels for clean and
distortion. In order to use the different amplifier channels, I replace the manual amp
footswitches with a MIDI controlled relay array that I built from a MSA kit by [Highly
Liquid](https://web.archive.org/web/20211220170920/http://www.highlyliquid.com/) (now
defunct, but the [code](https://github.com/staskevich/MIDIWidget-Firmware) is now open
source). This allows changing the amps between the clean and distortion channels by also
sending a patch change MIDI command to the relay array. This is the patch
`Amp_switcher.pd`.

All the remaining Pd patches are subpatches used by these two main patches.

There's obviously plenty more that can be done, perhaps most pending, triggering all of
these patch changes from a foot pedal controller. Again, plenty of ways this can be
achieved, particularly with commercial software, but I wanted to do this using a portable
open source event manager like Pd, and with sufficient UI so that manual overrides can be
performed in rehearsal & improvisation, without having everything locked down to a
particular patch for a "song".

Hope something of this can be helpful for others!

