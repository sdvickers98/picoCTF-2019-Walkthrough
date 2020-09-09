# plumbing
200 points

### Description
*"Sometimes you need to handle process data outside of a file. Can you find a way to keep the output from this program and search for the flag? Connect to 2019shell1.picoctf.com 63345"*

### Solution
If you connect to the provided address and port, you get a lot of text that looks something like this:
```
$ nc 2019shell1.picoctf.com 63345
...
This is defintely not a flag
This is defintely not a flag
This is defintely not a flag
Not a flag either
Not a flag either
This is defintely not a flag
Again, I really don't think this is a flag
I don't think this is a flag either
Not a flag either
Again, I really don't think this is a flag
Again, I really don't think this is a flag
I don't think this is a flag either
Not a flag either
I don't think this is a flag either
I don't think this is a flag either
I don't think this is a flag either
Not a flag either
Again, I really don't think this is a flag
Again, I really don't think this is a flag
Not a flag either
I don't think this is a flag either
Not a flag either
Not a flag either
Not a flag either
Again, I really don't think this is a flag
Again, I really don't think this is a flag
Again, I really don't think this is a flag
Not a flag either
```

However. if you actually search through that output using a pipe and `grep`, then we can find something more useful:
```
$ nc 2019shell1.picoctf.com 63345 | grep 'pico'
```

This should get you the flag. Just use Ctrl+C to terminate the netcat process.

<details>
  <summary>Flag:</summary>
  picoCTF{digital_plumb3r_4e7a5813}
</details>

[Next Problem](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/general_skills/%2313%20-%20whats-the-difference.md)

[Return to General Skills](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/general_skills/%230%20-%20General%20Skills%20Homepage.md)

[Return to Homepage](https://github.com/sdvickers98/picoCTF-2019-Walkthrough)
