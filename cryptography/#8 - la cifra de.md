# la cifra de
200 points

### Description
*"I found this cipher in an old book. Can you figure out what it says? Connect with nc 2019shell1.picoctf.com 12254."*

### Solution
Running the netcat command provided gives the following output:
```
Encrypted message:
Ne iy nytkwpsznyg nth it mtsztcy vjzprj zfzjy rkhpibj nrkitt ltc tnnygy ysee itd tte cxjltk

Ifrosr tnj noawde uk siyyzre, yse Bnretèwp Cousex mls hjpn xjtnbjytki xatd eisjd

Iz bls lfwskqj azycihzeej yz Brftsk ip Volpnèxj ls oy hay tcimnyarqj dkxnrogpd os 1553 my Mnzvgs Mazytszf Merqlsu ny hox moup Wa inqrg ipl. Ynr. Gotgat Gltzndtg Gplrfdo 

Ltc tnj tmvqpmkseaznzn uk ehox nivmpr g ylbrj ts ltcmki my yqtdosr tnj wocjc hgqq ol fy oxitngwj arusahje fuw ln guaaxjytrd catizm tzxbkw zf vqlckx hizm ceyupcz yz tnj fpvjc hgqqpohzCZK{m311a50_0x_a1rn3x3_h1ah3xf653pdkh}

Ehk ktryy herq-ooizxetypd jjdcxnatoty ol f aordllvmlbkytc inahkw socjgex, bls sfoe gwzuti 1467 my Rjzn Hfetoxea Gqmexyt.

Tnj Gimjyèrk Htpnjc iy ysexjqoxj dosjeisjd cgqwej yse Gqmexyt Doxn ox Fwbkwei Inahkw.

Tn 1508, Ptsatsps Zwttnjxiax tnbjytki ehk xz-cgqwej ylbaql rkhea (g rltxni ol xsilypd gqahggpty) ysaz bzuri wazjc bk f nroytcgq nosuznkse ol yse Bnretèwp Cousex.

Gplrfdo’y xpcuso butvlky lpvjlrki tn 1555 gx l cuseitzltoty ol yse lncsz. Yse rthex mllbjd ol yse gqahggpty fce tth snnqtki cemzwaxqj, bay ehk fwpnfmezx lnj yse osoed qptzjcs gwp mocpd hd xegsd ol f xnkrznoh vee usrgxp, wnnnh ify bk itfljcety hizm paim noxwpsvtydkse.
```

If you do some googling on the title, "la cifra de", you might find out about a cipher called the **Vigenère cipher** that was first described in a work by Giovan Battista Bellaso entitled *La cifra del Sig. Giovan Battista Bellaso*.

#### Vigenère cipher

The Vigenère cipher is a modified version of the Caesar cipher. Instead of always using the same value to shift characters by, the shift amount rotates through a repeating series of numbers. This series of repeating shift values is often represented by a keyword, or key. The place of each letter in the alphabet is the shift value that the letter represents (we treat the alphabet as if it's zero indexed, i.e. a = 0, b = 1, etc.).

Okay, if that wasn't a good enough explanation, here's an example. Say we have the message "HELLO" and the keyword "ABCDE". Then, we look consecutively at the letters of the message and the key, using the key to determine the value that each letter in the message should be shifted by.
* H + A = H + 0 = H
* E + B = E + 1 = F
* L + C = L + 2 = N
* L + D = L + 3 = O
* O + E = O + 4 = S

So, we get the resulting encrypted message: HFNOS. 

Note that the message and keyword do not need to be the same length. If the keyword is longer than the message, then just use characters of the keyword until the entire message is encrypted. If the message is longer than the keyword, then just repeat using the letters in the keyword.

Say we have the same message from earlier, "HELLO", and the keyword "ABC".
* H + A = H + 0 = H
* E + B = E + 1 = F
* L + C = L + 2 = N
* L + A = L + 0 = L
* O + B = O + 1 = P

And the result: HFNLP.

Cracking a Vigenère cipher is much more difficult than cracking a Caesar cipher. The best way to start is by trying to find the length of the key. This is often done by looking for repeated sequences of characters in the text. While this isn't true 100% of the time, these repeated sequences typically indicate words that are repeated in the message and just so happen to have been encrypted using the same part of the key multiple times.

Next, you should find the size of the gaps between occurrences of each sequence. Say that the characters "abc" show up four times in a Vigenère-encrypted message, and the gaps between consecutive occurrencences are of these sizes: 24, 36, and 18 (i.e. the second occurrence is 24 characters after the first, the third occurrence is 36 characters after the second, etc.). You must look for the common divisors of these numbers: 2, 3, and 6. So, one of these numbers (2, 3, 6) is most likely the length of the key in this example.

#### Back to this problem

There are a lot of great online tools that will help you crack a Vigenère cipher for you. In fact, websites like [this](https://www.boxentriq.com/code-breaking/vigenere-cipher) one will do most of the work for you, but I think [this](https://simonsingh.net/The_Black_Chamber/vigenere_cracking_tool.html) one is really worth checking out. It has great visualizations that really help with understanding the Vigenère cipher cracking process, and the website has a lot of other great cryptography information on it too. You can't decrypt any text with special characters though, so I've put a version of the message that you can you use with it below. The only characters that have been removed are characters that would have been skipped during the encryption anyways, so their removal does not impede the cracking process.
<details>
  <summary>Message:</summary>
NEIYNYTKWPSZNYGNTHITMTSZTCYVJZPRJZFZJYRKHPIBJNRKITTLTCTNNYGYYSEEITDTTECXJLTKIFROSRTNJNOAWDEUKSIYYZREYSEBNRETWPCOUSEXMLSHJPNXJTNBJYTKIXATDEISJDIZBLSLFWSKQJAZYCIHZEEJYZBRFTSKIPVOLPNXJLSOYHAYTCIMNYARQJDKXNROGPDOSMYMNZVGSMAZYTSZFMERQLSUNYHOXMOUPWAINQRGIPLYNRGOTGATGLTZNDTGGPLRFDOLTCTNJTMVQPMKSEAZNZNUKEHOXNIVMPRGYLBRJTSLTCMKIMYYQTDOSRTNJWOCJCHGQQOLFYOXITNGWJARUSAHJEFUWLNGUAAXJYTRDCATIZMTZXBKWZFVQLCKXHIZMCEYUPCZYZTNJFPVJCHGQQPOHZCZKMAXARNXHAHXFPDKHEHKKTRYYHERQOOIZXETYPDJJDCXNATOTYOLFAORDLLVMLBKYTCINAHKWSOCJGEXBLSSFOEGWZUTIMYRJZNHFETOXEAGQMEXYTTNJGIMJYRKHTPNJCIYYSEXJQOXJDOSJEISJDCGQWEJYSEGQMEXYTDOXNOXFWBKWEIINAHKWTNPTSATSPSZWTTNJXIAXTNBJYTKIEHKXZCGQWEJYLBAQLRKHEAGRLTXNIOLXSILYPDGQAHGGPTYYSAZBZURIWAZJCBKFNROYTCGQNOSUZNKSEOLYSEBNRETWPCOUSEXGPLRFDOYXPCUSOBUTVLKYLPVJLRKITNGXLCUSEITZLTOTYOLYSELNCSZYSERTHEXMLLBJDOLYSEGQAHGGPTYFCETTHSNNQTKICEMZWAXQJBAYEHKFWPNFMEZXLNJYSEOSOEDQPTZJCSGWPMOCPDHDXEGSDOLFXNKRZNOHVEEUSRGXPWNNNHIFYBKITFLJCETYHIZMPAIMNOXWPSVTYDKSE
</details>

These online crackers sometimes can't find the exact key, but they can usually get close enough that you can figure it out by inspecting the different keys that it tried and their associated outputs. There are often a few guessed keys that have the first few characters correct.


I could go a little more into this specific encrypted message, but I really think you should crack it using the second link I provided above. You'll understand the cipher and how to crack it much better that way.

If you can't figure out the key.
<details>
  <summary>Hint:</summary>
  The key is <b>flag</b>
</details>

And if you just want the flag.
<details>
  <summary>Flag:</summary>
  picoCTF{b311a50_0r_v1gn3r3_c1ph3ra653edec}
</details>

[Return to Cryptography](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/cryptography/%230%20-%20Cryptography%20Home%20Page.md)

[Return to Homepage](https://github.com/sdvickers98/picoCTF-2019-Walkthrough)
