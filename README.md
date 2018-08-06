Howdy y'all,

This is a quick URH project for my Eco-Worthy Multi-Purpose Motor
Forward Reverse Controller.  Your own controller might use a different
code, but both of mine happen to use the same sequences.


Perhaps you'll find it handy for practicing software defined radio, or
perhaps not.  I'm using these controllers for the HF screwdriver
antenna on my ham radio truck, and my only interest in the protocol
was to clone the protocol into my GoodWatch.

See this URL for the watch side of things.

https://github.com/travisgoodspeed/goodwatch/wiki/OOK_Example


73 from Knoxville,

--Travis KK4VCZ




## Buttons, Modes

The Digital Remote Controller that comes with the EcoWorthy motor
controller is a little white remote with a collapsible antenna and
four buttons: A, B, C and D.

A locks the motor moving forward, while B locks it moving backward.
There are also hardware buttons on the controller board for this.
Holding C steps the motor forward, while holding D steps it backward.

## Recordings, Interpretation

The transmitting remote drifts quite a bit.  Each symbol is either a
short bit (`8`) or a long bit (`e`), so I try to get the cleanest
digital description by adjusting the bit length until I get one
accurate decoding for each button.

`USRP-433_920MHz-1MSps-1MHz-buttona.complex` holds the A button.  At a
bit length of 545µs, a packet of `ee8e8e8e8e8e8e8e888888ee8` is
accurately decoded in ASK mode.


`USRP-433_920MHz-1MSps-1MHz-buttonb.complex` holds the B button.  At a
bit length of 530µs, a packet of `ee8e8e8e8e8e8e8e8888ee888` is
accurately decoded in ASK mode.


`USRP-433_920MHz-1MSps-1MHz-buttonc.complex` holds the C button.  At a
bit length of 530µs, a packet of `ee8e8e8e8e8e8e8e88ee88888` is
accurately decoded in ASK mode.

`USRP-433_920MHz-1MSps-1MHz-buttond.complex` holds the D button.  At a
bit length of 530µs, a packet of `ee8e8e8e8e8e8e8eee8888888` is
accurately decoded in ASK mode.


## Results

As of 6 August 2018, adding this to your `config.h` adds support for
directing the motor with a GoodWatch.  Refactoring will soon change
the exact style of the definition, but this should be plenty to get
you started.

```C
//Settings for the Eco-Worthy Digital Motor Controller.
//Rate is 341us.  Should be 450us, but that's close enough.
#define OOKMDMCFG4 0x86
#define OOKMDMCFG3 0xd9
#define OOKBUTTONA "\x00\xee\x8e\x8e\x8e\x8e\x8e\x8e\x8e\x88\x88\x88\xee\x80\x00\x00"
#define OOKBUTTONB "\x00\xee\x8e\x8e\x8e\x8e\x8e\x8e\x8e\x88\x88\xee\x88\x80\x00\x00"
#define OOKBUTTONC "\x00\xee\x8e\x8e\x8e\x8e\x8e\x8e\x8e\x88\xee\x88\x88\x80\x00\x00"
#define OOKBUTTOND "\x00\xee\x8e\x8e\x8e\x8e\x8e\x8e\x8e\xee\x88\x88\x88\x80\x00\x00"
```
