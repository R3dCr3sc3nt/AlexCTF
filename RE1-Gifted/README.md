# RE1 - Gifted

## Challenge
[gifted](gifted)

## Solution
This was a simple RE challenge, we started running the 'strings' command against the binary and immediately found the flag.

![Flag from strings](https://github.com/R3dCr3sc3nt/AlexCTF/blob/master/RE1-Gifted/strings.png)

If we disassemble the binary in radare2 we also see the flag being pushed as a string onto the stack just before the call to strcmp.

![Flag from radare2](https://github.com/R3dCr3sc3nt/AlexCTF/blob/master/RE1-Gifted/radare.png)

The flag is **AlexCTF{Y0u_h4v3_45t0n15h1ng_futur3_1n_r3v3r5ing}**
