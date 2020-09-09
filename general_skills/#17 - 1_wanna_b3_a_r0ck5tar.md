# 1_wanna_b3_a_r0ck5tar
350 points

### Description
*"I wrote you another song. Put the flag in the picoCTF{} flag format"*

# Solution
This is another program in the [rockstar programming language](https://codewithrockstar.com/) from the previous question:
```
Rocknroll is right              
Silence is wrong                
A guitar is a six-string        
Tommy's been down               
Music is a billboard-burning razzmatazz!
Listen to the music             
If the music is a guitar                  
Say "Keep on rocking!"                
Listen to the rhythm
If the rhythm without Music is nothing
Tommy is rockin guitar
Shout Tommy!                    
Music is amazing sensation 
Jamming is awesome presence
Scream Music!                   
Scream Jamming!                 
Tommy is playing rock           
Scream Tommy!       
They are dazzled audiences                  
Shout it!
Rock is electric heaven                     
Scream it!
Tommy is jukebox god            
Say it!                                     
Break it down
Shout "Bring on the rock!"
Else Whisper "That ain't it, Chief"                 
Break it down 
```

Okay, when we put this one into the compiler on the rockstar website, we don't get any output. So this time we'll need to understand what the code is doing. 

We can do this by reading the [documentation](https://codewithrockstar.com/docs) on the website to be able to understand the rockstar programming language, but could we translate this to something we are more familiar with, say, python?

Yes! [rockstar-py](https://github.com/yyyyyyyan/rockstar-py) will translate any file containing rockstar code into python code. We can install it using `pip`.
```
$ pip install rockstar-py
$ rockstar-py -i lyrics.txt -o lyrics.py
```

The `-i` and`-o` flags are used to specify the names of the input and output files. We'll have to clean up this code a bit to make it runnable. Here's what it should look like after cleaning it up (I've marked the lines I changed with dashes):
 ```python
Rocknroll = True
Silence = False
a_guitar = 10
Tommy = 44
Music = 170
the_music = input()
if the_music == a_guitar:
    print("Keep on rocking!")
    the_rhythm = input()
    if the_rhythm - Music == False:
        Tommy = 66
        print(Tommy) # ------------------------
        Music = 79
        Jamming = 78
        print(Music) # ------------------------
        print(Jamming) # ----------------------
        Tommy = 74
        print(Tommy) # ------------------------
        # They are dazzled audiences ----------
        print(it) # ---------------------------
        Rock = 86
        print(it) # ---------------------------
        Tommy = 73
        print(it) # ---------------------------
        # break -------------------------------
        print("Bring on the rock!")
    else:
        print("That ain't it, Chief")
        # break -------------------------------
 ```
 
It should be noted that the transpiler made a couple of mistakes. If you check out the documentation mentioned above, you can find out how numbers are defined in rockstar. The transpiler made a mistake when calculating the values to assign to two of these variables: `a_guitar` and `Music`. I'm not sure why it only got these two wrong but the correct values are `a_guitar = 136` and `Music = 1970`. 

These two variables won't actually matter because I'm gonna recommend that you just get rid of the if statements, or make them always true.

There's one specific mistake in the python code that I want to point out. If you read the rockstar documentation about [pronouns](https://codewithrockstar.com/docs#pronouns), you'll realize that the line "They are dazzled audiences" should actually translate to `Tommy = 79` since "they" is a reserved pronoun that refers to the named variable that was most recently used. "it" is another one of these reserved pronouns, so each `print(it)` statement should be printing the previously used named variable.

The break statements are just a way for the rockstar language to clarify the end of an if block. Since python figures this out through indentation, we can leave these commented out.

Here is the corrected python code:
```python
Rocknroll = True
Silence = False
a_guitar = 136 # ------------------------------
Tommy = 44
Music = 1970 # --------------------------------
the_music = input()
if True: # ------------------------------------
    print("Keep on rocking!")
    the_rhythm = input()
    if True:
        Tommy = 66
        print(Tommy) # ------------------------
        Music = 79
        Jamming = 78
        print(Music) # ------------------------
        print(Jamming) # ----------------------
        Tommy = 74
        print(Tommy) # ------------------------
        Tommy = 79
        print(Tommy) # ------------------------
        Rock = 86
        print(Rock) # -------------------------
        Tommy = 73
        print(Tommy) # ------------------------
        # break -------------------------------
        print("Bring on the rock!")
    else:
        print("That ain't it, Chief")
        # break -------------------------------
```

You just have to put in a couple random inputs, and you'll get the following sequence of numbers:
```
66
79
78
74
79
86
73
```

Like the previous problem, these are ASCII values, so we can put them in a file called `output.txt` and convert them to characters with python:
```python
with open('output.txt','r') as f:
    for line in f:
        print(chr(int(line)), end='')
    print()
```

Just put the flag in the picoCTF{} format like usual.

<details>
  <summary>Flag:</summary>
  picoCTF{BONJOVI}
</details>

This is the final General Skills question! These are some great questions for people who are less experienced with the linux command line, or at least less experienced with some of the commands that hackers commonly use to listen to connections, manipulate the content of files, etc. I hope you guys enjoyed these problems and refined your command line skills!

[Return to General Skills](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/general_skills/%230%20-%20General%20Skills%20Homepage.md)

[Return to Homepage](https://github.com/sdvickers98/picoCTF-2019-Walkthrough)
