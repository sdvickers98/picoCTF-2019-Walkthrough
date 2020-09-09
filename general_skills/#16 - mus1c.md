# mus1c
300 points

### Description
*"I wrote you a song. Put it in the picoCTF{} flag format"*

### Solution
Here's what that "song" file has in it:
```
Pico's a CTFFFFFFF
my mind is waitin
It's waitin

Put my mind of Pico into This
my flag is not found
put This into my flag
put my flag into Pico


shout Pico
shout Pico
shout Pico

My song's something
put Pico into This

Knock This down, down, down
put This into CTF

shout CTF
my lyric is nothing
Put This without my song into my lyric
Knock my lyric down, down, down

shout my lyric

Put my lyric into This
Put my song with This into my lyric
Knock my lyric down

shout my lyric

Build my lyric up, up ,up

shout my lyric
shout Pico
shout It

Pico CTF is fun
security is important
Fun is fun
Put security with fun into Pico CTF
Build Fun up
shout fun times Pico CTF
put fun times Pico CTF into my song

build it up

shout it
shout it

build it up, up
shout it
shout Pico
```

This one is...interesting. If you stare at this long enough, you may notice a lot of repetition and structure, almost like a programming language. 

Google "shout it programming language" and you should find something to run this program.

The program will output some numbers to you that might look like ASCII integer values. We can convert those easily using python:
```python
with open('output.txt','r') as f:
    for line in f:
        print(chr(int(line)), end='')
    print()
```

`output.txt` is just a text file that I copy and pasted the numbers from the output into. Put the output of this python code in the normal picoCTF flag 
format and you've got the flag.

<details>
  <summary>Flag:</summary>
  picoCTF{rrrocknrn0113r}
</details>

[Next Problem](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/general_skills/%2315%20-%20flag_shop.md)

[Return to General Skills](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/general_skills/%230%20-%20General%20Skills%20Homepage.md)

[Return to Homepage](https://github.com/sdvickers98/picoCTF-2019-Walkthrough)
