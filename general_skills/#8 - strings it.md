# strings it
100 points

### Description
*"Can you find the flag in file without running it? You can also find the file in /problems/strings-it_1_7a67382a38fc00751a6b9b29b0872813 on the shell server."*

### Solution
The title hints to use the linux command `strings`, which will print all continuous strings of printable characters within a file. 

If you run this command on the file that is provided, "strings", you will get quite a large output. To help us find the flag in this output, we should pipe it
into `grep`. This means we will use the output of `strings` as the input file for `grep 'pico'`.

This is done as following:
```
$ strings strings | grep 'pico'
```

<details>
  <summary>Flag:</summary>
  picoCTF{5tRIng5_1T_0690b2a5}
</details>

[Next Problem](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/general_skills/%239%20-%20what's%20a%20net%20cat%3F.md)

[Return to General Skills](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/general_skills/%230%20-%20General%20Skills%20Homepage.md)

[Return to Homepage](https://github.com/sdvickers98/picoCTF-2019-Walkthrough)
