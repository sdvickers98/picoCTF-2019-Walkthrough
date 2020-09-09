# where-is-the-file
200 points

### Description
*"I've used a super secret mind trick to hide this file. Maybe something lies in /problems/where-is-the-file_6_8eae99761e71a8a21d3b82ac6cf2a7d0."*

### Solution
If you login to the picoCTF server using `ssh` and `cd` to the directory mentioned in the problem, you'll fine a semmingly empty directory:
```
$ ls
$
```
If you know about hidden files though, you may think to use `ls` with the `-a` flag, for "all". This lists **all** files in the directory:
```
$ ls -a
.cant_see_me
```

Files and directories that begin with "." are typically hidden from the user and can only be seen when the user specifically asks for them to be shown. They
are typically used to store user preferences and configuration files.

You can view the contents of `.cant_see_me` using `cat .cant_see_me`.

<details>
  <summary>Flag:</summary>
  picoCTF{w3ll_that_d1dnt_w0RK_a88d16e4}
</details>

[Next Problem](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/general_skills/%2312%20-%20plumbing.md)

[Return to General Skills](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/general_skills/%230%20-%20General%20Skills%20Homepage.md)

[Return to Homepage](https://github.com/sdvickers98/picoCTF-2019-Walkthrough)
