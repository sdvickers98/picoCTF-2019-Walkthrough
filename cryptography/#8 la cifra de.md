# la cifra de
200 points

### Description
*"I found this cipher in an old book. Can you figure out what it says? Connect with nc 2019shell1.picoctf.com 12254."*

### Solution
Running the netcat command provided gives the following output:
```
Encrypted message:
﻿Encrypted message:
﻿Ne iy nytkwpsznyg nth it mtsztcy vjzprj zfzjy rkhpibj nrkitt ltc tnnygy ysee itd tte cxjltk

Ifrosr tnj noawde uk siyyzre, yse Bnretèwp Cousex mls hjpn xjtnbjytki xatd eisjd

Iz bls lfwskqj azycihzeej yz Brftsk ip Volpnèxj ls oy hay tcimnyarqj dkxnrogpd os 1553 my Mnzvgs Mazytszf Merqlsu ny hox moup Wa inqrg ipl. Ynr. Gotgat Gltzndtg Gplrfdo 

Ltc tnj tmvqpmkseaznzn uk ehox nivmpr g ylbrj ts ltcmki my yqtdosr tnj wocjc hgqq ol fy oxitngwj arusahje fuw ln guaaxjytrd catizm tzxbkw zf vqlckx hizm ceyupcz yz tnj fpvjc hgqqpohzCZK{m311a50_0x_a1rn3x3_h1ah3xf653pdkh}

Ehk ktryy herq-ooizxetypd jjdcxnatoty ol f aordllvmlbkytc inahkw socjgex, bls sfoe gwzuti 1467 my Rjzn Hfetoxea Gqmexyt.

Tnj Gimjyèrk Htpnjc iy ysexjqoxj dosjeisjd cgqwej yse Gqmexyt Doxn ox Fwbkwei Inahkw.

Tn 1508, Ptsatsps Zwttnjxiax tnbjytki ehk xz-cgqwej ylbaql rkhea (g rltxni ol xsilypd gqahggpty) ysaz bzuri wazjc bk f nroytcgq nosuznkse ol yse Bnretèwp Cousex.

Gplrfdo’y xpcuso butvlky lpvjlrki tn 1555 gx l cuseitzltoty ol yse lncsz. Yse rthex mllbjd ol yse gqahggpty fce tth snnqtki cemzwaxqj, bay ehk fwpnfmezx lnj yse osoed qptzjcs gwp mocpd hd xegsd ol f xnkrznoh vee usrgxp, wnnnh ify bk itfljcety hizm paim noxwpsvtydkse.
```

This one may be a bit tough if you aren't familiar with different ciphers you could try cracking. If you do some googling on the title, "la cifra de", you might find a cipher called the **Vigenère cipher** that was first described in a work by Giovan Battista Bellaso entitled *La cifra del Sig. Giovan Battista Bellaso*.

The Vigenère cipher is a modified version of the Caesar cipher. Instead of always using the same amount to shift characters by, the shift amount rotates through a repeating series of numbers. This series of repeating shift values is often represented by a keyword. The place of each letter in the alphabet (zero indexed, so a = 0) is the shift value that the letter represents.

Okay, if that wasn't a good enough explanation, here's an example. Say we have the message "hello" and the keyword "abcde". Then, we go consecutively through letters of the message and the key, using the key to determine the value that the letter should be shifted by.
* h + a = h + 0 = h
* e + b = e + 1 = f
* l + c = l + 2 = n
* l + d = l + 3 = o
* o + e = o + 4 = s

So, we get the resulting encrypted message: hfnos. 

Note that the message and keyword do not need to be the same length. If the keyword is longer than the message, then just use characters of the keyword until the entire message is encrypted. If the message is longer than the key, then just repeat using the letters in the key word.

Say we have the same message from earlier, "hello", and the keyword "abc".
* h + a = h + 0 = h
* e + b = h + 1 = f
* l + c = l + 2 = n
* l + a = l + 0 = l
* o + b = 0 + 1 = p

And the result: hfnlp.
