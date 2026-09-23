# test scripts

## Enumerate monitors using ZEP

This script enumerates the monitors using ZEP-2.x. It prints some basic information
about the heads. This script also displays a window on each of the heads (up to 6
heads at the moment).

This script makes it possible to ignore setting a window on certain heads.

e.g. head 2 or head 2 and 3 can be ignored using the following commands:

```bash
zep-2.7 enummonitors.zp --i 2
zep-2.7 enummonitors.zp --ignore-heads 23
```

So use the `--i ` or `--ignore-heads` option to specify heads on which you don't
want to display a window. This might be useful when displays are cloned for example.
The clone will display a window anyway, and a second might make stuff more difficult.
Commandline option parsing is not straightforward with zep, so 23 means monitors two
and three. The option value just takes a string, and when the head number (as string)
is present in the option_value of --i the head will be ignored.
So when having more than 10 monitors, option parsing will likely have some need
of tender care.

You can use the script zepdpyinfo (that comes with zep) to get a list with heads too,
but that won't display a window on (a) head(s).

One of the short comings of zep is that it doesn't display know/exposes which head is
the primary. So use arandr or similar to extract that information.

## testing audio

You can use the zep script **zepsound.zp** to play a fragment of audio that will
demonstrate where each channel will end up. As the channels are 0-indexed in zep,
the audio will play a speech fragment "zero" on channel zero an fragment "n" on each
following channels where "n" is the nth channel.

Since you probably want to specify the sound card/interface and the number of channels
(up to 10 channels are supported 0-9) you want to consider the following options:

- `--d` or `--device`` to specify wich device you want to use
- `--n` or `--num-channels` to specify the number of channels you want to use.

So in order to run a sound on 4 different channels on the motu M6 given the following
output of zepsndinfo:
```bash
$ zepsndinfo
Sound system ALSA:
    device 0 [HDA Intel PCH: ALC3204 Analog (hw:0,0)]: (preferred input/output/duplex)
         input channels:    2
         output channels:   2
         sampling rates:    44100, 48000
    device 1 [HDA Intel PCH: HDMI 0 (hw:0,3)]:
         input channels:    0
         output channels:   2
         sampling rates:    32000, 44100, 48000
    device 2 [HDA Intel PCH: HDMI 1 (hw:0,7)]:
         input channels:    0
         output channels:   2
         sampling rates:    32000, 44100, 48000
    device 3 [HDA Intel PCH: HDMI 2 (hw:0,8)]:
         input channels:    0
         output channels:   8
         sampling rates:    32000, 44100, 48000, 88200, 96000, 176400, 192000
    device 4 [HDA Intel PCH: HDMI 3 (hw:0,9)]:
         input channels:    0
         output channels:   8
         sampling rates:    32000, 44100, 48000, 88200, 96000, 176400, 192000
    device 5 [M6: USB Audio (hw:1,0)]:
         input channels:    6
         output channels:   0
         sampling rates:    
```

You would have to run the command as:
```bash
$zep zepsound.zp --d=5 --n=4
```

** Note:** The motu channels are 1 indexed, we use 0 indexed values as those
are used by the zep programming language
