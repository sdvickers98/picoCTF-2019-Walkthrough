# First Grep: Part II
200 points

### Description
*"Can you find the flag in /problems/first-grep--part-ii_3_b4bf3244c2886de1566a28c1b5a465ae/files on the shell server? Remember to use grep."*

### Solution
If you haven't used the picoCTF shell server by now, you'll have to for this problem. To do that, run `ssh username@2019shell1.picoctf.com` replacing "username"
with your username, and enter your password when prompted. Then use `cd /problems/first-grep--part-ii_3_b4bf3244c2886de1566a28c1b5a465ae/` to go to the
directory with our problem files (sorry if you already know how to do all of this).

"files" is just a directory with other directories of files. Instead of searching through them manually, we can use `grep` recursively.
```
$ grep -r 'pico' files
```

This will search every file under "files" in the directory hierarchy for occurences of the string "pico".

<details>
  <summary>Flag:</summary>
  picoCTF{grep_r_to_find_this_3675d798}
</details>

[Next Problem](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/general_skills/%2312%20-%20plumbing.md)

[Return to General Skills](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/general_skills/%230%20-%20General%20Skills%20Homepage.md)

[Return to Homepage](https://github.com/sdvickers98/picoCTF-2019-Walkthrough)
