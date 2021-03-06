# miniRSA
300 points

### Description
*"Lets decrypt this: ciphertext? Something seems a bit small"*

### Solution
The problem provides a text file containing the following:
```
N: 29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673
e: 3

ciphertext (c): 2205316413931134031074603746928247799030155221252519872649594750678791181631768977116979076832403970846785672184300449694813635798586699205901153799059293422365185314044451205091048294412538673475392478762390753946407342073522966852394341 
```
This is an example of very weak RSA encryption because *e* is so small. If you want to know more specifics about RSA encryption, I go into more detail about it in my [walkthough](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/cryptography/%239%20-%20rsa-pop-quiz.md) for the previous problem.

Whenever *e* is too small, you run the risk of *c ≡ m<sup>e</sup>* being smaller than *n*. This is bad because anyone can just find the "*e*'th root" of *c* in the integers to decipher the message. We can do this in python easily, but we'll need to use a module called [gmpy](https://gmpy2.readthedocs.io/en/latest/intro.html). These numbers are larger than what python can normally handle, but gmpy is designed to do arithmetic with large numbers so it helps us get around that. 
```python
import gmpy
from Crypto.Util.number import long_to_bytes

n = 29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673
e = 3
c = 2205316413931134031074603746928247799030155221252519872649594750678791181631768977116979076832403970846785672184300449694813635798586699205901153799059293422365185314044451205091048294412538673475392478762390753946407342073522966852394341  

root, exact = gmpy.root(c, e)
print(long_to_bytes(root).decode())
```
**Note:** This is another one of those problems where your ciphertext and flag are unique to you. So, make sure you're doing this with **your** version of the ciphertext.

**Note:** The `exact` variable above is just the second thing in the tuple that's returned by the `root` function. It's a boolean that is true if the root is exact, and false otherwise.

This is why it's dangerous to have a small *e*. Shorter messages end up with values of *m<sup>e</sup>* that are smaller than *n*, so the modular arithmetic part of RSA encryption becomes irrelevant.

Remember, your flag is unique to you in this problem, but here's the format it should be in. The X's are placeholders for the random characters that are unique to your flag.
<details>
  <summary>Flag:</summary>
  picoCTF{n33d_a_lArg3r_e_XXXXXXXX}
</details>

[Next Problem](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/cryptography/%2311%20-%20waves%20over%20lambda.md)

[Return to Cryptography](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/cryptography/%230%20-%20Cryptography%20Home%20Page.md)

[Return to Homepage](https://github.com/sdvickers98/picoCTF-2019-Walkthrough)
