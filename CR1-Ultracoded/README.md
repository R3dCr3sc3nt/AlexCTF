# CR1 - Ultracoded

## Challenge
> Fady didn't understand well the difference between encryption and encoding, so instead of encrypting some secret message to pass to his friend, he encoded it!

> Hint: Fady's encoding doens't handly any special character

[zero_one](zero_one)

## Solution
The zero_one is a text file containing patterns of "ZERO" and "ONE". I figured this must be converted to a binary representation so I wrote a small python script to do this. (I will show snippets of the script, the libraries are used later in the write-up)

```
#!/usr/bin/python2.7
import binascii
import base64

data = open("zero_one").read()
dataArr = data.split()
binaryBuffer = ""

for w in dataArr:
  if "ZERO" in w:
    binaryBuffer += "0"
  if "ONE" in w:
    binaryBuffer += "1"
```
I converted the buffer string to integer and used the unhexlify() function in the binascii library to return me the ASCII plaintext.
```
n = int(binaryBuffer, 2)
binDecoded = binascii.unhexlify('%x' % n)
```
Printing the output gave me a base64 encoded string.
```
Li0gLi0uLiAuIC0uLi0gLS4tLiAtIC4uLS4gLSAuLi4uIC4tLS0tIC4uLi4uIC0tLSAuLS0tLSAuLi4gLS0tIC4uLi4uIC4uLSAuLS0uIC4uLi0tIC4tLiAtLS0gLi4uLi4gLiAtLi0uIC4tLiAuLi4tLSAtIC0tLSAtIC0uLi0gLQ==
```
Using the base64 library I decoded the base64 string
```
base64Decoded = base64.b64decode(binDecoded)
```
Printing this output gave me an output resembling morse code
```
.- .-.. . -..- -.-. - ..-. - .... .---- ..... --- .---- ... --- ..... ..- .--. ...-- .-. --- ..... . -.-. .-. ...-- - --- - -..- -
```
I couldn't find a library to decode morse code so I used built the decoded string from a python dictionary
```
CODE = {'.-': 'A',    '-...': 'B',  '-.-.': 'C',
        '-..': 'D',   '.': 'E',     '..-.': 'F',
        '--.': 'G',   '....': 'H',  '..': 'I',
        '.---': 'J',  '-.-': 'K',   '.-..': 'L',
        '--': 'M',    '-.': 'N',    '---': 'O',
        '.--.': 'P',  '--.-': 'Q',  '.-.': 'R',
        '...': 'S',   '-': 'T',     '..-': 'U',
        '...-': 'V',  '.--': 'W',   '-..-': 'X',
        '-.--': 'Y',  '--..': 'Z',

        '-----': '0', '.----': '1', '..---': '2',
        '...--': '3', '....-': '4', '.....': '5',
        '-....': '6', '--...': '7', '---..': '8',
        '----.': '9'
        }

morseDecoded = ''.join(CODE.get(i) for i in base64Decoded.split())
```
Printing the output gave me something closely resembling the flag format. 
```
ALEXCTFTH15O1SO5UP3RO5ECR3TOTXT
```
The hint in challenge description mentioned that special characters weren't handled so after some experimentation I determined that the O's were underscores and that the curly brackets were simply missing. Here's the final part of the python script.
```
morseList = list(morseDecoded.lower())

alexCTF = ''.join(morseList[0:7])
flag = ""

for l in morseList[7:]:
    if "o" in l:
        flag += "_"
    else:
        flag += l

print "The flag is: " + alexCTF + "{" + flag + "}"
```
And the output and solution
```
The flag is: alexctf{th15_1s_5up3r_5ecr3t_txt}
```



