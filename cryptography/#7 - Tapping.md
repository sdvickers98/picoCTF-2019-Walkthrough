# Tapping
200 points

### Description
*"Theres tapping coming in from the wires. What's it saying nc 2019shell1.picoctf.com 32273."*

### Solution
If you've heard of or worked with **netcat**, you may recognize the command at the end of the prompt. Netcat is a utility for reading from and writing to network connections, and it comes with most distributions of linux. You can go [here](https://www.linuxfordevices.com/tutorials/netcat-command-in-linux) for some good info on netcat. 

The command above tells netcat to listen to 2019shell.picoctf.com on port 32273. If you run this command in a shell (picoCTF provides a linux server that you can use), you'll
get the following output:

.--. .. -.-. --- -.-. - ..-. { -- ----- .-. ... ...-- -.-. ----- -.. ...-- .---- ... ..-. ..- -. .---- -.... --... --... ..--- ..... --... ..--- ---.. --... }

The brackets are a clear indicator that this is an encrypted version of the flag, and you probably recognize this form of encryption as **Morse code**. If you want to decipher
this by hand, you can visit the [Wikipedia](https://en.wikipedia.org/wiki/Morse_code) page. But like I say, a good hacker should take advantage of all available resources, so 
here's a [website](https://morsecode.world/international/translator.html) that will translate the Morse code message for you.

<details>
  <summary>Flag:</summary>
  PICOCTF{M0RS3C0D31SFUN1677257287}
</details>

[Next Problem](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/cryptography/%238%20-%20la%20cifra%20de.md)

[Return to Cryptography](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/cryptography/%230%20-%20Cryptography%20Home%20Page.md)

[Return to Homepage](https://github.com/sdvickers98/picoCTF-2019-Walkthrough)
