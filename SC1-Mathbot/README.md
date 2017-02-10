# SC1 - Math bot

## Challenge
> It is well known that computers can do tedious math faster than humans.

> nc 195.154.53.62 1337

## Solution
```
$ nc 195.154.53.62 1337
                __________
         ______/ ________ \______
       _/      ____________      \_
     _/____________    ____________\_
    /  ___________ \  / ___________  \
   /  /XXXXXXXXXXX\ \/ /XXXXXXXXXXX\  \
  /  /############/    \############\  \
  |  \XXXXXXXXXXX/ _  _ \XXXXXXXXXXX/  |
__|\_____   ___   //  \\   ___   _____/|__
[_       \     \  X    X  /     /       _]
__|     \ \                    / /     |__
[____  \ \ \   ____________   / / /  ____]
     \  \ \ \/||.||.||.||.||\/ / /  /
      \_ \ \  ||.||.||.||.||  / / _/
        \ \   ||.||.||.||.||   / /
         \_   ||_||_||_||_||   _/
           \     ........     /
            \________________/

Our system system has detected human traffic from your IP!
Please prove you are a bot
Question  1 :
50489238639188063698070072981610 * 1364107478925961178712787264169 =
```

I reconnected a few times to confirm that the server handed out random equations to be solved. After solving one manually, I was prompted with a new math problem. At this point, I wrote a python script to automate the process.

```
#!/usr/bin/python2.7
import socket

host = '195.154.53.62'
port = 1337

bot = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
bot.connect((host,port))

while True:

    data = bot.recv(1024)

    if "=" in str.split(data)[-1]:    
        equation = str.split(data)[-4] + " " + str.split(data)[-3] + " " + str.split(data)[-2]

        print "Solving equation..."
        print equation

        result = repr(eval(equation))

        print "Sending result..."
        bot.send(result + "\n")

    else:
        print data
        break
```

Running the script returns the flag after a few seconds.

```
Solving equation...
77570593763924035994006787070091 * 156048715378978225422935000952364
Sending result...
Well no human got time to solve 500 ridiculous math challenges
Congrats MR bot!
Tell your human operator flag is: ALEXCTF{1_4M_l33t_b0t}
```
