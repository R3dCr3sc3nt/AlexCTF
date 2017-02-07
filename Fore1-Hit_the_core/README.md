# Fore1: Hit the core

## Challenge
[fore1.core](fore1.core)

## Solution
Running the 'strings' command against the file gives us a bunch of output but one line in particular stands out.
```
** snip **

AWAVA
AUATL
[]A\A]A^A_
cvqAeqacLtqazEigwiXobxrCrtuiTzahfFreqc{bnjrKwgk83kgd43j85ePgb_e_rwqr7fvbmHjklo3tews_hmkogooyf0vbnk0ii87Drfgh_n kiwutfb0ghk9ro987k5tfb_hjiouo087ptfcv}
;*3$"
(q9e

** snip **
```

Judging by the curly brackets in one of the lines, we figured the flag might be extracted from this. Upon closer inspection it becomes clear that every fifth character starting from the first A spells ALEXCTF, perhaps this correlation continues throughout? We wrote a python script to check.

```
#!/usr/bin/python2.7
data = "cvqAeqacLtqazEigwiXobxrCrtuiTzahfFreqc{bnjrKwgk83kgd43j85ePgb_e_rwqr7fvbmHjklo3tews_hmkogooyf0vbnk0ii87Drfgh_n kiwutfb0ghk9ro987k5tfb_hjiouo087ptfcv}"
flag = ""

for i in range(len(data)):
  if (i-3)%5 == 0:
    flag += data[i]
  else:
    continue

print flag
```

Sure enough the flag is returned **ALEXCTF{K33P_7H3_g00D_w0rk_up}**
