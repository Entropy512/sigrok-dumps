These are dumps from a Sony E-mount camera/lens.

These were taken using a modified 16mm Meike extension tube that brings out each lens contact
to a 10-pin ribbon cable

Pinout of the mount is as follows (These pins are from left to right looking at a lens from the rear):
1: LENS_GND - Lens motor GND

2: LENS_POWER - Lens motor power.  Can be either 5.0v or unregulated Vbat (7.4v nominal) - This is somehow
negotiated between body and lens

3: LOGIC_GND - Ground for lens logic circuitry

4: BODY_VD_LENS - As-of-yet unknown body->lens signalling.  In nearly all cases, is normally high
but pulses low at a very low duty cycle at 60 Hz (is it 50 in EU?)

5: LOGIC_VCC - Lens logic power.  3.15v  All data lines described below are 3.15v logic high

6: LENS_CS_BODY - Handshaking line from lens to body.  Always high when RXD is transferring data, normally low

7: RXD - Serial data from lens to body.  Starts at 750 kbaud, usually negotiates up to 1.5 Mbaud during init.  8N1 lsb-first

8: TXD - Serial data from body to lens.  Same speeds as above

9: BODY_CS_LENS - Handshaking line from body to lens.  Always high when TXD is transferring data

10: LENS_XDETECT - (weakly) pulled high by the body.  Grounded to LOGIC_GND by the lens, or sometimes via
680 ohm resistor (Viltrox EF-NEX II).  Used to detect presence of a lens.  Body will not output power
unless this is grounded.

In all attached captures, only BODY_VD_LENS, LOGIC_VCC, LENS_CS_BODY, RXD, TXD, and BODY_CS_LENS were
monitored in that order.

Sample rate was 6 MHz using an fx2lafw board - http://www.amazon.com/gp/product/B00ZOC23TK - This 
appears to be identical to the LCSoft Mini Board - http://sigrok.org/wiki/Lcsoft_Mini_Board

Protocol (quick summary):
Data is only transmitted when a CS line goes high.  Only one frame of data is transmitted per
high CS period.  All frames start with 0xF0, followed by a command ID byte.  All frames end with
0x55, this is preceded by a 16-bit checksum of the command ID byte plus all payload bytes.  Checksum
is least significant byte first.  Frames from body to lens are sometimes padded with additional 0x00
bytes beyond 0x55.

A CS line can go high without any data being transmitted.  This has so far only been seen during a speed
change.

The protocol appears to assume fixed frame lengths for a given command ID.  Occurrences of 0x55 within
a frame are NOT escaped.

During "idle" operation, a low pulse of BODY_VD_LENS appears to trigger two status response frames
from the lens to the body, followed by two frames from body to lens.


Summary of hardware used

Body : Sony ILCE-A6000

Probe breakout: Meike 16mm macro extension tube with all pins wired out to a ribbon cable

Lenses :

Sony SEL55210 55-210mm zoom lens, initialization captured at both 55mm and 210mm zoom settings

Viltrox EF-NEX II adapter - Canon EF to Sony E mount electronic adapter

Canon EF 50mm/1.8 STM - Used with Viltrox adapter

Canon EF-S 24mm/2.8 STM - Used with Viltrox adapter

Sony SELP1650 16-50mm Power Zoom lens - Initialization only captured at the lens' default power-on
focal length due to PZ + retractable lens

More details can be found in the dpreview thread at:
http://www.dpreview.com/forums/post/56133485
