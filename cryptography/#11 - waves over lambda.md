# waves over lambda
300 points

### Description
*"We made alot of substitutions to encrypt this. Can you decrypt it? Connect with nc 2019shell1.picoctf.com 45185."*

### Solution
Running the netcat command gives us this:
```
-------------------------------------------------------------------------------
vrebsoqx hwsw ux krzs dmob - dswazwevk_ux_v_rcws_moygpo_yzlblweerp
-------------------------------------------------------------------------------
omwfwk dkrprsrcuqvh tosoyojrc iox qhw qhusp xre rd dkrprs locmrcuqvh tosoyojrc, o moep riews iwmm terie ue rzs puxqsuvq ue hux rie pok, oep xqumm swywygwswp oyreb zx riueb qr hux bmrryk oep qsobuv pwoqh, ihuvh hollwewp qhusqwwe kwosx obr, oep ihuvh u xhomm pwxvsugw ue uqx lsrlws lmovw. drs qhw lswxweq u iumm remk xok qhoq qhux moepriewsdrs xr iw zxwp qr vomm huy, omqhrzbh hw hospmk xlweq o pok rd hux mudw re hux rie wxqoqwiox o xqsoebw qklw, kwq rew lswqqk dswazweqmk qr gw ywq iuqh, o qklw ognwvq oep cuvurzx oep oq qhw xoyw quyw xwexwmwxx. gzq hw iox rew rd qhrxw xwexwmwxx lwsxrex ihr osw cwsk iwmm vologmw rd mrrtueb odqws qhwus irsmpmk oddousx, oep, ollosweqmk, odqws erqhueb wmxw. dkrprs locmrcuqvh, drs uexqoevw, gwboe iuqh ewfq qr erqhueb; hux wxqoqw iox rd qhw xyommwxq; hw soe qr puew oq rqhws ywe'x qogmwx, oep doxqwewp re qhwy ox o qropk, kwq oq hux pwoqh uq ollwoswp qhoq hw hop o hzepswp qhrzxoep srzgmwx ue hosp voxh. oq qhw xoyw quyw, hw iox omm hux mudw rew rd qhw yrxq xwexwmwxx, doeqoxquvom dwmmrix ue qhw ihrmw puxqsuvq. u swlwoq, uq iox erq xqzlupuqkqhw yonrsuqk rd qhwxw doeqoxquvom dwmmrix osw xhswip oep ueqwmmubweq werzbhgzq nzxq xwexwmwxxewxx, oep o lwvzmuos eoqureom drsy rd uq.
```

If you've taken physics before, you may recall that the the velocity of a wave, *v*, divided by the wavelength of the wave, *λ*, is equal to the frequency of the wave, *f*, 
i.e. *f = v / λ*. That's what the title "waves over lambda" is hinting at: frequency.

We should try frequency analysis on this cipher. If we throw it in [this](https://simonsingh.net/The_Black_Chamber/vigenere_cracking_tool.html) tool that I recommended in my
walkthrough of the Vigenère cipher problem, we don't really get anywhere. 

We know the cipher uses subsitution, but it isn't a type of shift cipher. We also have a title telling us that we can use frequency analysis to help us crack the cipher. This 
hints that we are probably dealing with a **cryptogram**. 

Cryptograms are usually short puzzles in which you must break a cipher where every letter is replaced by a different letter. This differs from the Caesar cipher because the 
substituted letters are not always a fixed amount to the left or right of the letter being replaced. So, these are a little hard to crack than a Caesar cipher. However, cryptograms are often easier to crack than Vigenère ciphers because each letter will always have the same substitute letter. In a Vigenère cipher, each letter has a number of different substitute letters equal to the length of the key. 

There's a good cryptogram cracker [here](https://www.boxentriq.com/code-breaking/cryptogram). This one also gives you the option to try to crack the cipher by hand. The best way
to do this is by looking for repeated words that are up to four or five letters (contractions are good ones) and guessing what specific letters substitutions are. It's a lot of trial and error, but it can be a lot of fun.

This gets us the flag, and you just need to fill in the spaces with underscores.
<details>
  <summary>Flag:</summary>
  picoCTF{frequency_is_c_over_lambda_mupgpennod}
</details>

[Return to Cryptography](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/cryptography/%230%20-%20Cryptography%20Home%20Page.md)

[Return to Homepage](https://github.com/sdvickers98/picoCTF-2019-Walkthrough)
