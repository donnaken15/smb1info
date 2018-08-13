# Super Monkey Ball hacking info

## ELF contents

(doltool info)
`BSS Address:      801ED920
BSS Size:         00104ED5

Entry Point:      80003100

Text Section  0:  Offset=00000100  Address=80003100  Size=000023C0
Text Section  1:  Offset=000024C0  Address=800065A0  Size=001092C0

Data Section  0:  Offset=0010B780  Address=800054C0  Size=000006C0
Data Section  1:  Offset=0010BE40  Address=80005B80  Size=00000A20
Data Section  2:  Offset=0010C860  Address=8010F860  Size=00000020
Data Section  3:  Offset=0010C880  Address=8010F880  Size=00000020
Data Section  4:  Offset=0010C8A0  Address=8010F8A0  Size=00062AE0
Data Section  5:  Offset=0016F380  Address=80172380  Size=0007B5A0
Data Section  6:  Offset=001EA920  Address=802F01E0  Size=00001900
Data Section  7:  Offset=001EC220  Address=802F2800  Size=00004480`

Theme arrangement:
The address that sets themes for each level is located at 0x1B6AF0.
The format is simple, each byte sets the theme of a stage based
on the offset of the byte. Here's what Super Monkey Ball's theme
array looks like:
0D0D0D0D0F0F0F0F0F01
0D0D0D0D... and so on

So if you were to change the first byte,
that would change the theme for the first stage.

Theme list:
`0 = NULL                    }

1 = TYPE A / Sky             }

2 = TYPE B / Night           }

3 = TYPE C / Sunset          }

4 = TYPE D / Water           }

5 = TYPE E / Storm           } - Monkey Ball themes

6 = TYPE F / Ice             }

7 = TYPE G / Sand            }

8 = TYPE H / Space           }

9 = TYPE I / Cave            }

A = TYPE J / Bonus / Master  }

B = E3 (unknown)

C = Jungle

D = Water

E = Night

F = Sun

10 = Space

11 = Sand

12 = Ice

13 = Storm

14 = Bonus

15 = Pilot (crashes if stage isn't already a Monkey Target level)

16 = Billiards

17 = Golf

18 = Bowling

19 = Master

1A = Ending`

You can also find this using Test Mode.

Challenge mode:

The address for this can be found at 0x1B7730.

Most of it is already explained via SMB Level Workshop Discord,
but one thing about the stage time is that the value is stored in
a short byte, so if the value goes over 0x7FFF, the time faults
back to zero, even resulting in the timer explosion animation
happening right before the player can move.

# /test/

This section doesn't go into far analysis
of the files but just a quick explanation of how
they're used and what they represent.

- The "preview" folder contains pictures for practice mode/race
track thumbnails and next-level images that appear from the sky.
- CRASH_STAR appears many times in a few common model files.
- SMB levels use .gma and .tpl to create the level model, while
the original Monkey Ball levels use st???_p.lz and st???.lz.
- Stage 190 (in debug) is used for the main menu.
- The intro depends on Stage 99, 71, 61, 101, Advanced 3, Beginner 10,
Advanced 11, Expert 40 (last bonus).
- When playing music, the game will repeatedly read from the music file
(if you were to use procmon.exe, you will see) instead of completely
loading it into memory, so if the file is deleted, it will still try
to read from it, but you will hear nothing, until the file is put back
into place.
- The folder labeled "stage" is Beginner 1 and is used in
test mode for various tests.
- st000 is empty and is never used.

# Dialog format

This feature is what I call AVTEXT, and it works like this:

usage:
?/text(/)

Normal text:
a/text

Bold text:
b/a/text

Colored text:
c/0xff0000/a/text

Picture:
p/NAME/

Button A: p/BUTTON_A/
Button B: p/BUTTON_B/
etc.

Arrows:
Left: p/SANNKAKU_L/
Up: p/SANNKAKU_U/
Down: p/SANNKAKU_D/
Right: p/SANNKAKU_R/

D-pad: p/BUTTON_+/

Camera-Stick: p/LEVEL/

San(n)kaku means Triangulate in Japanese

Japanese/Katana:
h/non-katana text
k/idk what this is yet

Special special (like actual Japanese letters or accent letters)
characters used in a/ texts breaks the game.
