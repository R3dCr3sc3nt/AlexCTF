# RE1 - Gifted

## Challenge
[gifted](gifted)

## Solution
The challenge is simply a link to an ELF binary. After downloading the binary, run `strings` to look for anything interesting.

```
$ strings gifted
/lib/ld-linux.so.2
libc.so.6
_IO_stdin_used
exit
...
[^_]
AlexCTF{Y0u_h4v3_45t0n15h1ng_futur3_1n_r3v3r5ing}
Enter the flag:
You got it right dude!
Try harder!
;*2$"
...
```

The flag is quickly found a plaintext string in the binary. For further investigation, I disassembled the binary in [radare2](https://github.com/radare/radare2). The flag being pushed as a string onto the stack just before the call to `strcmp`.

![Flag from radare2](https://github.com/R3dCr3sc3nt/AlexCTF/blob/master/RE1-Gifted/radare.png)

The flag is **AlexCTF{Y0u_h4v3_45t0n15h1ng_futur3_1n_r3v3r5ing}**.
