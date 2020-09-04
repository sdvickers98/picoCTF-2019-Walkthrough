# caesar
*"Decrypt this message. You can find the ciphertext in /problems/caesar_2_10e2c1660e7b34790d93f61a1e4dd9d9 on the shell server."*

The message provided is "picoCTF{ynkooejcpdanqxeykjrnpavoth}". 

The hint here is in the name: caesar. The **Caesar cipher** is one of the most well-known and simple encryption techniques available. Each letter in the message is 
shifted to the left or right by a fixed number of positions in the alphabet. For example, with a left-shift of 3, the message "hello" would be encrypted as "ebiil".

You could write a script to print out all 25 possible shifts, but a good hacker always takes advantage of the resources that are available. If you check out 
[this](https://www.dcode.fr/caesar-cipher) website, you can use their Caesar cipher decoder to see all possible shifts and figure out which one makes the most sense
as the flag.

If you're having trouble figuring out what the shift is, you can find out below.
<details>
  <summary>Hint:</summary>
  The shift is +22, or a right shift by 22. This is the same thing as a left shift by 4.
</details>

And if you're super lazy and just want to see the flag.
<details>
  <summary>Flag:</summary>
  picoCTF{crossingtherubiconvrtezsxl}
</details>

[Return to Cryptography](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/cryptography/%230%20-%20Cryptography%20Home%20Page.md)

[Return to Homepage](https://github.com/sdvickers98/picoCTF-2019-Walkthrough)
