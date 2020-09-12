# picoCTF 2019 Walkthrough

Welcome to my walkthrough of picoCTF 2019! CTFs, or "Capture The Flag" games, involve (legally) hacking into a system or systems to obtain a flag or number of flags. These flags are just pieces of text that can only be viewed by exploiting some vulnerability in the system that was purposefully left by the creators of the CTF. If you aren't familiar with picoCTF, here's an excerpt from the [picoCTF website](https://picoctf.com) about the game:

>picoCTF is a free computer security game targeted at middle and high school students, created by security experts at Carnegie Mellon University. The game consists of a series of challenges centered around a unique storyline where participants must reverse engineer, break, hack, decrypt, or do whatever it takes to solve the challenge. 

No worries if you're older than middle and high school students. If you're a newbie to hacking, it's never too late to get interested in computer security, and picoCTF is a great game to help you develop the basic practical skills you'll need to get started. If you're already a skilled hacker, you can likely still find challenging problems in picoCTF that will interest you, since it has problems related to many different areas of cyber security. 

I've tried to make this walkthrough very detailed. When I decided to make this, I didn't want it to to be a "copy this code and you'll get the flag" kind of walkthrough. There are several places where I provide code to solve the problem, but I also go into detail about the concepts behind each problem, what the code is doing, and why we want it to do that. In places where I don't explain *every* detail, I provide links for those who are interested in more information about the topic. 

This walkthrough isn't just a resource where you can figure out how to solve these specific problems, but rather a resource where you can learn the main ideas and concepts behind each problem so that you can figure out similar problems on your own in the future. Just think of the walkthrough as a "basics of hacking" class that uses picoCTF as the class workbook. Don't worry, I'm not giving lectures here, but some of the problems do require quite of bit of explanation for you understand them.

All that being said, I've divided all of the solutions for picoCTF just like the game does it: based on their category. The categories are:
* [General Skills](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/general_skills/%230%20-%20General%20Skills%20Homepage.md)
* [Cryptography](https://github.com/sdvickers98/picoCTF_Walkthroughs/blob/master/cryptography/%230%20-%20Cryptography%20Home%20Page.md)
* [Binary Exploitation](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/binary_exploitation/%230%20-%20Binary%20Exploitation%20Homepage.md)
* Forensics
* Reverse Engineering
* Web Exploitation

You can choose to do the problems in whatever order of category you like. 

**NOTE:** All of the categories will be available from the beginning of the game, but you will have to do most of the problems within each category in sequential order.

Don't feel like you need to follow the walkthrough for every problem! Many of the problems are written in such a way as to give hints to their solution. You'll make greater progress by only resorting to this walkthrough and others like it as a last resort. You'll get better at finding useful information (or as we say it, you'll improve your "google-fu"), which is a skill that every resourceful hacker needs to have. I hope you have fun playing picoCTF and make huge improvements to your hacking skills!

**NOTE:** The flag of every picoCTF problem is in one of two formats: picoCTF{*flag*}, picoCTF{*FLAG*} or PICOCTF{*FLAG*}. Most problems use the first format, and problems that don't will usually make a note of it in a hint.

P.S. : Thanks so much for checking this out. If you find any mistakes, or want to contact me for any other reason, give me an email at sdvickers98@gmail.com.

Keep Hacking,

Dakota Vickers
