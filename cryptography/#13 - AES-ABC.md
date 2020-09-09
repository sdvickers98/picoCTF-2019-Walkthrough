# AES-ABC
400 points

### Description
*"AES-ECB is bad, so I rolled my own cipher block chaining mechanism - Addition Block Chaining! You can find the source here: aes-abc.py. The AES-ABC flag is body.enc.ppm"*

### Solution
The problem gives us a file called body.enc.ppm along with the python source code that was used to encrypt it:
```python
#!/usr/bin/env python

from Crypto.Cipher import AES
from key import KEY
import os
import math

BLOCK_SIZE = 16
UMAX = int(math.pow(256, BLOCK_SIZE))


def to_bytes(n):
    s = hex(n)
    s_n = s[2:]
    if 'L' in s_n:
        s_n = s_n.replace('L', '')
    if len(s_n) % 2 != 0:
        s_n = '0' + s_n
    decoded = s_n.decode('hex')

    pad = (len(decoded) % BLOCK_SIZE)
    if pad != 0: 
        decoded = "\0" * (BLOCK_SIZE - pad) + decoded
    return decoded


def remove_line(s):
    # returns the header line, and the rest of the file
    return s[:s.index('\n') + 1], s[s.index('\n')+1:]


def parse_header_ppm(f):
    data = f.read()

    header = ""

    for i in range(3):
        header_i, data = remove_line(data)
        header += header_i

    return header, data
        

def pad(pt):
    padding = BLOCK_SIZE - len(pt) % BLOCK_SIZE
    return pt + (chr(padding) * padding)


def aes_abc_encrypt(pt):
    cipher = AES.new(KEY, AES.MODE_ECB)
    ct = cipher.encrypt(pad(pt))

    blocks = [ct[i * BLOCK_SIZE:(i+1) * BLOCK_SIZE] for i in range(len(ct) / BLOCK_SIZE)]
    iv = os.urandom(16)
    blocks.insert(0, iv)
    
    for i in range(len(blocks) - 1):
        prev_blk = int(blocks[i].encode('hex'), 16)
        curr_blk = int(blocks[i+1].encode('hex'), 16)

        n_curr_blk = (prev_blk + curr_blk) % UMAX
        blocks[i+1] = to_bytes(n_curr_blk)

    ct_abc = "".join(blocks)
 
    return iv, ct_abc, ct


if __name__=="__main__":
    with open('flag.ppm', 'rb') as f:
        header, data = parse_header_ppm(f)
    
    iv, c_img, ct = aes_abc_encrypt(data)

    with open('body.enc.ppm', 'wb') as fw:
        fw.write(header)
        fw.write(c_img)
```
So, a file called "flag.ppm" was encrypted using this source code and then given to us as "body.enc.ppm".

You've probably thought by now to google "AES" or "AES-ECB", and if you have then you're on the right track. But before we talk about that, we need to talk about block ciphers.

By the way, I'm going to talk about the math behind this stuff a little bit, so if you already know about it or just don't want to know about the math, 
you can <a href="#back_to_problem">skip</a> to when I start talking about this problem again. However, if you don't know the math behind it, you won't really understand 
*why* we are doing the things that we do.

#### Block Ciphers
A **block cipher** is a cryptographic algorithm that operates on **blocks** of a fixed bit-size, *n*. Block ciphers have an associated secret **key**, *K*, of size *k* 
bits that is used to encrypt and decrypt messages. The cipher must also have an associated encryption function *E<sub>K</sub>(P)*, where *P* is a block of size *n*, 
and this function must be [bijective](https://en.wikipedia.org/wiki/Bijection).

So, *E* bijectively maps pairs of *k*-bit long strings and *n*-bit long strings, *(K, P)*, to *n*-bit long strings, *C*. In other words, for every key *K* of size 
*k* and block *P* of size *n*, there is a *unique* block *C* of size *n* that *K* and *P* are mapped to.

Since *E* is bijective, it must have an inverse function *D*, that also maps pairs of *k*-bit long strings and *n*-bit long strings to *n*-bit long strings. To be
the inverse of *E*, i.e. *D = E<sup>-1</sup>*, *D* must satisfy *D<sub>K</sub>(E<sub>K</sub>(P)) = P* for all values of *K*, given *P*.

**Note:** Since *E* is bijective, the encryption *E<sub>K</sub>(P)* will be different for every value of *K*, even if *P* is fixed.

*D* is the decryption function since it reverses the encryption done to *P*. You can look [here](https://en.wikipedia.org/wiki/Block_cipher) for more info on block ciphers.

#### Advanced Encryption Standard
The **Advanced Encryption Standard** (AES) is a type of block cipher that uses a fixed block size, *n*, of 128 bits (16 bytes) and a key size, *k*, of 128, 192, or 256 bits. AES is 
an iterative block cipher, which means that *E<sub>K</sub>* is applied to *P* for several **rounds**. The number of rounds in AES is determined by the key size:
* 10 rounds for 128-bit keys
* 12 rounds for 192-bit keys
* 14 rounds for 256-bit keys

The AES encryption function is typically described through several encryption processing steps. There will also be an associated set of decryption steps. These are just the
functions *E* and *D* being broken down into steps for algorithmic simplicity.

The AES needs to generate a separate 128-bit key for each round, plus an initial key. These keys are generated from a main cipher key using the 
[AES key schedule](https://en.wikipedia.org/wiki/AES_key_schedule).

The math behind the AES is a little dense, but it basically consists of substitution and permutation. I would go into more detail about it here, but the AES
[Wikipedia](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard#High-level_description_of_the_algorithm) page has a good explanation of the algorithm.
If you'd rather learn by watching than reading, check out [this](https://www.youtube.com/watch?v=O4xNJsjtN6E) Computerphile video about the AES algorithm. I highly recommend that you check out at least one of these resources and make sure you understand the algorithm before continuing.

<h4 id="back_to_problem">Back to the problem</h4>

There are a few variants of the AES algorithm, but we often call them **modes of operation**. These are just different algorithms that block ciphers can use.
You can learn more about the most popular modes of operation [here](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Common_modes).

The problem mentions an AES mode: AES-ECB. This is the mode that is used to create the cipher in this line from the code above: `cipher = AES.new(KEY, AES.MODE_ECB)`.

ECB, or **electronic codebook**, is a block cipher algorithm where each block is encrypted independently using the same key. So, patterns of plaintext that are the same
will be encrypted to the same pattern of ciphertext. This makes it very easy to crack with frequency analysis.

By the way, have you googled the ".ppm" file extension yet? You'll find that ppm stands for **portable pixmap**, and that it is a type of image file. If you haven't
ever seen an image encrypted with AES-ECB, it looks something like this (credit to [this](https://blog.filippo.io/the-ecb-penguin/) post for the image):

![Tux-ECB-small.png](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/raw/Tux-ECB-small.png)

You can pretty clearly see what the image is because of how weak ECB is. Okay, hold that thought.

So, the python code above just applies the AES-ECB encryption to each block of the image file's bits, then does a rolling encryption effect. Essentially, each line will be the 
sum  of its ECB ciphertext and the ECB ciphertext of every block that came before it. So, the last block will be the sum of the ECB ciphertexts from each block. 

Have you tried viewing that "body.enc.ppm" image yet? If you can't figure out how to view it, you can use [gimp](https://www.gimp.org/).
You might notice that the pixels look more cluttered in the vertical center of the image. That's because of the rolling effect taking place in an area where the actual content
of the image is.

If we can undo the rolling process, then we can get image file that was encrypted using only normal ECB, and that might be enough to solve this problem.
Here's how we can do that in python:
```python
from Crypto.Util.number import long_to_bytes, bytes_to_long
import math
import sys

BLOCK_SIZE = 16
UMAX = int(math.pow(256, BLOCK_SIZE))

in_file = open("body.enc.ppm", "rb")
out_file = open("body.ppm", "wb")

data = in_file.read()
data = data.split(b"\n")
headers = b'\n'.join(data[:3])
cipher = b'\n'.join(data[3:])
blocks = [cipher[i * BLOCK_SIZE:(i+1) * BLOCK_SIZE] for i in range(len(cipher) // BLOCK_SIZE)]

image = b""

prev_block = 0
for b in blocks:
	block = long_to_bytes((bytes_to_long(b) - prev_block) % UMAX)
	image += block
	prev_block = bytes_to_long(b)

out_file.write(b'\n'.join(headers.split(b" ")) + b'\n' + image)
```
You should be able to see the flag if you view the newly decrypted image file. It will look like the image above, "encrypted" but still easy to tell what the image is supposed to be.

<details>
  <summary>Flag:</summary>
  picoCTF{d0Nt_r0ll_yoUr_0wN_aES}
</details>

[Next Problem](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/cryptography/%2314%20-%20b00tl3gRSA3.md)

[Return to Cryptography](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/cryptography/%230%20-%20Cryptography%20Home%20Page.md)

[Return to Homepage](https://github.com/sdvickers98/picoCTF-2019-Walkthrough)
