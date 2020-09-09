# whats-the-difference
200 points

### Description
*"Can you spot the difference? kitters cattos. They are also available at /problems/whats-the-difference_0_00862749a2aeb45993f36cc9cf98a47a on the shell server"*

### Solution
Usually, to see differences between two files, we would use `diff`. This is a really useful command to know, even if you aren't in security, so you can look at
the [man page](https://man7.org/linux/man-pages/man1/diff.1.html) if you want to learn more about it. 

If we use `diff` with the two files provided by the problem, we get this:
```
$ diff cattos.jpg kitters.jpg 
Binary files cattos.jpg and kitters.jpg differ
```

This is because these are binary image files. To compare files byte by byte, we want to use `cmp` instead of `diff`. 

If we look at the [man page](https://man7.org/linux/man-pages/man1/cmp.1.html) for `cmp`, we see that the `-b` flag will print the differing bytes,
and `-l` will print the byte numbers that differ and the actual values that differ. 

If we run this command using these two flags on the provided files, we get this:
```
$ cmp -bl cattos.jpg kitters.jpg
  49734 160 p    231 M-^Y
  49735 151 i    235 M-^]
  49736 143 c    230 M-^X
  49737 157 o    310 M-H
  87663 103 C     12 ^J
 162650 124 T    364 M-t
 175231 106 F    153 k
 175232 173 {    261 M-1
 211986 164 t    230 M-^X
 211987 150 h    222 M-^R
 211988  63 3     15 ^M
 211989 171 y    330 M-X
 284427 162 r    122 R
 292340  63 3    174 |
 292341 137 _    371 M-y
 331830 141 a    216 M-^N
 331831  65 5    365 M-u
 426632 137 _    346 M-f
 439903 144 d    360 M-p
 515770  61 1    112 J
 515771 146 f    252 M-*
 583608 146 f    341 M-a
 640996  63 3    310 M-H
 688795 162 r     77 ?
 688796  63 3    107 G
 702943 156 n     23 ^S
 751424 164 t    243 M-#
 754731 137 _     61 1
 754732  64 4    113 K
 754733 163 s    274 M-<
 754734 137 _    304 M-D
 796226 142 b     43 #
 871159 165 u    256 M-.
 871160  67 7      6 ^F
 871161  67 7    316 M-N
 871162  63 3    346 M-f
 927506 162 r    347 M-g
 927507 137 _    212 M-^J
 927508  64 4    122 R
 994666 156 n    376 M-~
 994667 144 d     43 #
 994668 137 _    377 M-^?
1068577 152 j    234 M-^\
1068578  63 3    344 M-d
1068579  61 1    203 M-^C
1068580  61 1    222 M-^R
1068581 171 y    162 r
1101444 137 _      5 ^E
1101445 141 a    173 {
1101446 163 s      7 ^G
1101447 154 l    300 M-@
1171017 153 k     53 +
1171018 152 j    147 g
1171019 146 f    356 M-n
1241182 144 d     51 )
1241183 163 s    224 M-^T
1241184 141 a    200 M-^@
1241185 154 l    106 F
1272572 153 k    217 M-^O
1272573 146 f    156 n
1337150 163 s      4 ^D
1410459 154 l    345 M-e
1410460 153 k    340 M-`
1460208 146 f      5 ^E
1510914 154 l    237 M-^_
1567157 153 k    322 M-R
1567158 152 j    100 @
1567159 144 d     42 "
1567160 163 s    220 M-^P
1567161 146 f    205 M-^E
1581925 144 d    315 M-M
1581926 163 s    244 M-$
1581927 172 z    215 M-^M
1581928 155 m    147 g
1581929 172 z    257 M-/
1677065  61 1    176 ~
1677066  60 0    341 M-a
1764510  65 5    357 M-o
1764511  64 4    210 M-^H
1764512  70 8     31 ^Y
1766742 175 }     13 ^K
```

You can see the flag in there, and we can get it manually from this output if we want, but there's a better way to do this. 

I'll use this as an opportunity to introduce the `awk` command, which can manipulate text by looking for certain patterns. It's commonly used to search
and manipulate text outputs that are presented in columns.

The characters that make up the flag are in the third column of the output. Let's pretend that this output is in a file called `output.txt`. To read the file 
line-by-line, printing only the third column, we can use `awk '{print $3}' output.txt`, where `$3` is telling the command to print the third column of each line.

In the previous example, the expression`{print $3}` is what's called an **AWK program**. It's actually a very simple program written in the AWK language, a 
language used for text manipulation. Instead of passing in the AWK program in-line, a file containing a multi-line AWK program can be passed in. You can
read more about `awk` on the [man page](https://man7.org/linux/man-pages/man1/awk.1p.html).

We still aren't quite ready to read the flag. I want this to be as easy as possible, a simple copy and paste. If we pipe the `cmp` command into the `awk` command 
we just learned (i.e. `cmp -bl cattos.jpg kitters.jpg | awk '{print $3}'), we will get those characters in the flag printed out one per line.

To get rid of these newline characters, I'll introduce one more command: `tr`. This command, which is short for "translate", can be used to substitute or remove
characters from text. If we check the [man page](https://man7.org/linux/man-pages/man1/tr.1.html), we see that the `-d` flag can be used to delete the specified 
character(s).

In this case, we want to get rid of newline characters: `tr -d '\n' *file*`. However, we do want a newline at the very end, so our command-line prompt isn't on
the same line as the output. This can be easily done by adding `; echo` to the end of the command.
```
$ cmp -bl cattos.jpg kitters.jpg | awk '{print $3}' | tr -d '\n'; echo
```

<details>
  <summary>Flag:</summary>
  picoCTF{th3yr3_a5_d1ff3r3nt_4s_bu773r_4nd_j311y_aslkjfdsalkfslkflkjdsfdszmz10548}
</details>

[Next Problem](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/general_skills/%2312%20-%20plumbing.md)

[Return to General Skills](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/general_skills/%230%20-%20General%20Skills%20Homepage.md)

[Return to Homepage](https://github.com/sdvickers98/picoCTF-2019-Walkthrough)
