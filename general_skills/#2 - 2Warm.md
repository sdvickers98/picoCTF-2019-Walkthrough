# 2Warm
50 points

# Description
*"Can you convert the number 42 (base 10) to binary (base 2)?"*

# Solution
I'm not going to go too deep into the binary number system. If you aren't familiar with it already, you can find a pretty intuitive tutorial [here](https://www.mathsisfun.com/binary-number-system.html) that will help you become familiar with binary numbers.

You can do this really easily in python:
```python
bin(42)
```
And we get the output `0b101010`.

We could also do this by hand. The easiest way to do this is to repeatedly subtract the largest possible power of 2 from 42. 

We start off with 2<sup>5</sup> = 32 since the next highest power of 2, 64, is larger than 42. 42 - 32 = 10. The next lowest power is 16, but this 
is larger than 10 so we get a 0 for 16.

Right now we have a 1 for 32 and a 0 for 16. 

8 is smaller than 10 so it gets a 1. 10 - 8 = 2. The next power is 4, but it's bigger than 2, so it gets a 0. 

2 is equal to 2, so it gets a 1. 2 - 2 = 0. 

There's nothing left to check, so 1 gets a 0.

Alltogether, we have 101010.

<details>
  <summary>Flag:</summary>
  picoCTF{101010}
</details>

[Return to General Skills](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/general_skills/%230%20-%20General%20Skills%20Homepage.md)

[Return to Homepage](https://github.com/sdvickers98/picoCTF-2019-Walkthrough)
