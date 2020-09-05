# rsa-pop-quiz
200 points

### Description
*"Class, take your seats! It's PRIME-time for a quiz... nc 2019shell1.picoctf.com 49989"*

### Solution
Running the command provided gives the following output:
```
Good morning class! It's me Ms. Adleman-Shamir-Rivest
Today we will be taking a pop quiz, so I hope you studied. Cramming just will not do!
You will need to tell me if each example is possible, given your extensive crypto knowledge.
Inputs and outputs are in decimal. No hex here!
#### NEW PROBLEM ####
q : 60413
p : 76753
##### PRODUCE THE FOLLOWING ####
n
IS THIS POSSIBLE and FEASIBLE? (Y/N):
```
So, the user is prompted for an answer. If you already know the answer, go ahead and keep taking the quiz. If you don't know the answer, then we're going to have to do some learnin' using our usual method: Google.

#### RSA Encryption
Googling "rsa" or "Adleman-Shamir-Rivest" will take you to the main [Wikipedia page](https://en.wikipedia.org/wiki/RSA_(cryptosystem)) for the **RSA** system of encryption. Notice that "Adleman-Shamir-Rivest" in reverse creates the acronym "RSA". These are the last names of the creators of RSA encryption.

RSA is a type of **public-key cryptography**, also knows as asymmetric cryptography. In simple terms, a public-key ecryption system requires that each person that wants to receive messages using the system has an associated public key and private key. The public key is used to encrypt, the private key is used to decrpyt.

Let's say Bob is using a public-key encryption system to receive secret messages. Bob has a public key and private key assoicated with him. The public key is, well, public. It can be used by anyone to encrypt a message for Bob, but the message can only be decrypted by Bob, using the private key.

Okay, I'm going to go pretty deep into the woods about RSA encryption. I'll try to provide links as much as possible so this doesn't get too long-winded. If you already know how RSA encryption works or just don't care to find out (I really hope it's the former), then you can just <a href="#back_to_problem">skip</a> to the part relevant to this problem, though you might not understand *why* we are doing some things.

RSA encryption is related to [modular arithmetic](https://en.wikipedia.org/wiki/Modular_arithmetic). I won't go too much into modular arithmetic, but the main thing you need to know is that two numbers are *equivalent modulo n* if they give the same remainder when divided by *n*. If we call the two numbers *a* and *b*, this relationship can also be shown through the expression "*a ≡ b (mod n)*", read "*a* is congruent to *b* mod *n*".

This concept is often used in programming with the **modulo operator**, "%". The expression `a % n` returns the value of *a* modulo *n*, i.e. the remainder of `a / n`.

This key expression is behind the RSA algorithm: *(m<sup>e</sup>)<sup>d</sup> ≡ m (mod n)*.

If we think in terms of encrypting a message, *m* represents the value of the character being encrypted, *e* and *n* represent the public key, and *d* represents the private key.

If *d* and *n* are very large positive integers, it can be very difficult to find *d* even if you know *n* and *e* and even *m*. I won't go too much into the math behind it, but it's related to how difficult it is to try all combinations of prime factors for very large numbers. You can look [here](https://certauth.epfl.ch/rsa/) for some of the more nitty gritty math if you're interested.

There are four main steps to the using the RSA system: key generation, key distribution, encryption, and decription.

##### Key Generation
Two random, very large prime numbers, *p* and *q* are chosen and multiplied together to get *n*. *n* is part of the public key, but *p* and *q* are kept secret.

Compute *λ(n) = lcm(p − 1, q − 1)* (This equivalency takes a lot of work to actually prove, you're going to want to take my word for it). This is called **Carmichael's totient function**. You can look more into it [here](https://en.wikipedia.org/wiki/Carmichael_function).

Choose *e* such that *1 < e < λ(n)* and *e* and *n* are **coprime**, i.e. *gcd(e, λ(n)) = 1. As mentioned before, *e* is part of the public key.

Determine *d* as the modular multiplicative inverse of *e* modulo *λ(n)*, i.e. solve for *d* in the equation *de ≡ 1 (mod λ(n))*. Remember,*d* is the private key.

So, the public parts are *e* and *n*. The private part is *d*, but *p*,*q*, and *λ(n)* must also be kept private since they are used to compute *d*.

##### Key Distribution
If Alice wants to send Bob an RSA-encrypted message, she must first have his public key *(n, e)*. He can transmit this to her any way he likes, it doesn't need to be secure since anyone who wants to decipher the message will still need the private key.

##### Encryption
So, Alice has obtained *(n, e)* from Bob and she wants to send him an encrypted message. She must first convert *m* to an integer less than *n* using what's known as a [padding scheme](https://en.wikipedia.org/wiki/Padding_(cryptography)). 

She then takes the new *m* and converts it to the ciphertext *c* using *n* and *e*: *c ≡ m<sup>e</sup> (mod n)*.

##### Decryption
When Bob receives the ciphertext from Alice, he can decrypt it using *d*, the private key: *c<sup>d</sup> ≡ (m<sup>e</sup>)<sup>d</sup> ≡ m (mod n)*.

Now Bob just needs to reverse the padding scheme on *m*, and he'll have the message!

<h4 id="back_to_problem">Back to the problem</h4>

So the prompt we were given after using the netcat command was this:
```
Good morning class! It's me Ms. Adleman-Shamir-Rivest
Today we will be taking a pop quiz, so I hope you studied. Cramming just will not do!
You will need to tell me if each example is possible, given your extensive crypto knowledge.
Inputs and outputs are in decimal. No hex here!
#### NEW PROBLEM ####
q : 60413
p : 76753
##### PRODUCE THE FOLLOWING ####
n
IS THIS POSSIBLE and FEASIBLE? (Y/N):
```

We now know what *p*,*q*, and *n* are referring to. We know that *n* is just the product of *p* and *q*. So, it is clearly possible to produce *n* in this example since we can just multiply *p* and *q*. 

If we answer "Y", we are given this prompt:
```
#### TIME TO SHOW ME WHAT YOU GOT! ###
n:
```

We know what to do: *n = p x q = 76753 x 60413 = **4636878989***.

Once we answer that one correctly, we're given this prompt:
```
Outstanding move!!!


#### NEW PROBLEM ####
p : 54269
n : 5051846941
##### PRODUCE THE FOLLOWING ####
q
IS THIS POSSIBLE and FEASIBLE? (Y/N):
```

Once again, we know *n = p x q*, so *q = n / p*. So, yes, it is possible. The next prompt:
```
#### TIME TO SHOW ME WHAT YOU GOT! ###
q:
```

*q = 5051846941 / 54269 = **93089***. Next, please:
```
Outstanding move!!!


#### NEW PROBLEM ####
e : 3
n : 12738162802910546503821920886905393316386362759567480839428456525224226445173031635306683726182522494910808518920409019414034814409330094245825749680913204566832337704700165993198897029795786969124232138869784626202501366135975223827287812326250577148625360887698930625504334325804587329905617936581116392784684334664204309771430814449606147221349888320403451637882447709796221706470239625292297988766493746209684880843111138170600039888112404411310974758532603998608057008811836384597579147244737606088756299939654265086899096359070667266167754944587948695842171915048619846282873769413489072243477764350071787327913
##### PRODUCE THE FOLLOWING ####
q
p
IS THIS POSSIBLE and FEASIBLE? (Y/N):
```
Okay, we know that you shouldn't be able to figure out *q* and *p* from *e* and *n*, otherwise RSA encryption wouldn't be secure at all. While this may technically be possible, it's not really feasible, especially without special hardware. Next prompt:
```
Outstanding move!!!


#### NEW PROBLEM ####
q : 66347
p : 12611
##### PRODUCE THE FOLLOWING ####
totient(n)
IS THIS POSSIBLE and FEASIBLE? (Y/N):
```
We talked about *totient(n)*, but we called it *λ(n)* and said that it was equivalent to *lcm(p − 1, q − 1)*. 

In this case, that's *lcm(66346, 12610) = **418311530***. I used [this](https://www.calculatorsoup.com/calculators/math/lcm.php) Least Common Multiple calculator to find the answer.

Wait, that one didn't work???

This is actually not a huge deal. The original [paper](https://people.csail.mit.edu/rivest/Rsapaper.pdf) describing RSA encryption uses a different totient function from the one I introduced. They used the **Euler totient function**: *φ(n) = (p − 1)(q − 1)*. 

Either one od these totient functions can be used for RSA encryption, since it can be shown that any *d* satisfying *d⋅e ≡ 1 (mod φ(n))* also satisfies *d⋅e ≡ 1 (mod λ(n))*. The one I introduced is more commonly used nowadays for reasons I won't really get into. Let's just say that RSA encryption works better when *d < λ(n)*, and *λ(n)* is a better totient function than *φ(n)* for satisfying that condition.

So, if we try this new totient function, we get the correct answer: *φ(n) = (p − 1)(q − 1) = 66346 x 12610 = **836623060***. Next prompt:
```
Outstanding move!!!


#### NEW PROBLEM ####
plaintext : 6357294171489311547190987615544575133581967886499484091352661406414044440475205342882841236357665973431462491355089413710392273380203038793241564304774271529108729717
e : 3
n : 29129463609326322559521123136222078780585451208149138547799121083622333250646678767769126248182207478527881025116332742616201890576280859777513414460842754045651093593251726785499360828237897586278068419875517543013545369871704159718105354690802726645710699029936754265654381929650494383622583174075805797766685192325859982797796060391271817578087472948205626257717479858369754502615173773514087437504532994142632207906501079835037052797306690891600559321673928943158514646572885986881016569647357891598545880304236145548059520898133142087545369179876065657214225826997676844000054327141666320553082128424707948750331
##### PRODUCE THE FOLLOWING ####
ciphertext
IS THIS POSSIBLE and FEASIBLE? (Y/N):
```
We know that to encrypt a message with RSA encryption, we just need the public key *(n, e)* and the message. So, yes, we can produce the cipher text: *c ≡ m<sup>e</sup> (mod n)*.

This is done pretty easyily in python:
```python
m = 6357294171489311547190987615544575133581967886499484091352661406414044440475205342882841236357665973431462491355089413710392273380203038793241564304774271529108729717
e = 3
n = 29129463609326322559521123136222078780585451208149138547799121083622333250646678767769126248182207478527881025116332742616201890576280859777513414460842754045651093593251726785499360828237897586278068419875517543013545369871704159718105354690802726645710699029936754265654381929650494383622583174075805797766685192325859982797796060391271817578087472948205626257717479858369754502615173773514087437504532994142632207906501079835037052797306690891600559321673928943158514646572885986881016569647357891598545880304236145548059520898133142087545369179876065657214225826997676844000054327141666320553082128424707948750331
c = pow(m, e, n)
print(c)
```
Here's the ciphertext if you don't want to run the script.
<details>
  <summary>Ciphertext:</summary>
256931246631782714357241556582441991993437399854161372646318659020994329843524306570818293602492485385337029697819837182169818816821461486018802894936801257629375428544752970630870631166355711254848465862207765051226282541748174535990314552471546936536330397892907207943448897073772015986097770443616540466471245438117157152783246654401668267323136450122287983612851171545784168132230208726238881861407976917850248110805724300421712827401063963117423718797887144760360749619552577176382615108244813
</details>

Next prompt:
```
Outstanding move!!!


#### NEW PROBLEM ####
ciphertext : 107524013451079348539944510756143604203925717262185033799328445011792760545528944993719783392542163428637172323512252624567111110666168664743115203791510985709942366609626436995887781674651272233566303814979677507101168587739375699009734588985482369702634499544891509228440194615376339573685285125730286623323
e : 3
n : 27566996291508213932419371385141522859343226560050921196294761870500846140132385080994630946107675330189606021165260590147068785820203600882092467797813519434652632126061353583124063944373336654246386074125394368479677295167494332556053947231141336142392086767742035970752738056297057898704112912616565299451359791548536846025854378347423520104947907334451056339439706623069503088916316369813499705073573777577169392401411708920615574908593784282546154486446779246790294398198854547069593987224578333683144886242572837465834139561122101527973799583927411936200068176539747586449939559180772690007261562703222558103359
##### PRODUCE THE FOLLOWING ####
plaintext
IS THIS POSSIBLE and FEASIBLE? (Y/N):
```
We know this isn't possible. *(n, e)* is the public key anyways, so it's nothing special to know that, and you can't produce the plaintext without *d*. Next:
```
Outstanding move!!!


#### NEW PROBLEM ####
q : 92092076805892533739724722602668675840671093008520241548191914215399824020372076186460768206814914423802230398410980218741906960527104568970225804374404612617736579286959865287226538692911376507934256844456333236362669879347073756238894784951597211105734179388300051579994253565459304743059533646753003894559
p : 97846775312392801037224396977012615848433199640105786119757047098757998273009741128821931277074555731813289423891389911801250326299324018557072727051765547115514791337578758859803890173153277252326496062476389498019821358465433398338364421624871010292162533041884897182597065662521825095949253625730631876637
e : 65537
##### PRODUCE THE FOLLOWING ####
d
IS THIS POSSIBLE and FEASIBLE? (Y/N):
```
We know *d* is determined as a number satisfying *de ≡ 1 (mod λ(n))*. We are given *e*, and we can find out *λ(n)* using *p* and *q*. So, yes, this is possible.
```
#### TIME TO SHOW ME WHAT YOU GOT! ###
d: 
```
Since we used the Euler totient function earlier, we will probably want to use instead of * it here too: *de ≡ 1 (mod φ(n))*. This is equivalent to *d ≡ e<sup>-1</sup> (mod φ(n))*.

We can find the modular inverse of a number using the python module [PyCrypto](https://github.com/pycrypto/pycrypto). Here's how we do that:
```python
from Crypto.Util.number import inverse

q = 92092076805892533739724722602668675840671093008520241548191914215399824020372076186460768206814914423802230398410980218741906960527104568970225804374404612617736579286959865287226538692911376507934256844456333236362669879347073756238894784951597211105734179388300051579994253565459304743059533646753003894559
p = 97846775312392801037224396977012615848433199640105786119757047098757998273009741128821931277074555731813289423891389911801250326299324018557072727051765547115514791337578758859803890173153277252326496062476389498019821358465433398338364421624871010292162533041884897182597065662521825095949253625730631876637
e = 65537
phi = (p - 1) * (q - 1)
d = inverse(e, phi)
print(d)
```
Here it is.
<details>
  <summary><i>d</i>:</summary>
1405046269503207469140791548403639533127416416214210694972085079171787580463776820425965898174272870486015739516125786182821637006600742140682552321645503743280670839819078749092730110549881891271317396450158021688253989767145578723458252769465545504142139663476747479225923933192421405464414574786272963741656223941750084051228611576708609346787101088759062724389874160693008783334605903142528824559223515203978707969795087506678894006628296743079886244349469131831225757926844843554897638786146036869572653204735650843186722732736888918789379054050122205253165705085538743651258400390580971043144644984654914856729
</details>

Next prompt:
```
Outstanding move!!!


#### NEW PROBLEM ####
p : 153143042272527868798412612417204434156935146874282990942386694020462861918068684561281763577034706600608387699148071015194725533394126069826857182428660427818277378724977554365910231524827258160904493774748749088477328204812171935987088715261127321911849092207070653272176072509933245978935455542420691737433
ciphertext : 17712948302053968160337608808023765353713891487724504165710075800666176704275900270871131114252105275962867934935572601922131269231577652839874752278037120009042079114201440532529424282349775046830004126930931418790562922816147664822871476098418888441696782597264107603520215924140671864491508516555630119132820414262583115708142593728022851982531082194761937261873838830778405312620786370902097963783652483624611685252621820304116460797923537545175795133241570733730324869356742756474956593641308168807758853188030625975084213572477077655289967561799083034525042713829515144782123152608246868892673838596163063470464
e : 65537
n : 23952937352643527451379227516428377705004894508566304313177880191662177061878993798938496818120987817049538365206671401938265663712351239785237507341311858383628932183083145614696585411921662992078376103990806989257289472590902167457302888198293135333083734504191910953238278860923153746261500759411620299864395158783509535039259714359526738924736952759753503357614939203434092075676169179112452620687731670534906069845965633455748606649062394293289967059348143206600765820021392608270528856238306849191113241355842396325210132358046616312901337987464473799040762271876389031455051640937681745409057246190498795697239
##### PRODUCE THE FOLLOWING ####
plaintext
IS THIS POSSIBLE and FEASIBLE? (Y/N):
```
What do we need to decipher an RSA-encrypted message? Well, *c<sup>d</sup> ≡ m (mod n)*, so we just need the ciphertext, *d*, and *n*. We are given the ciphertext and *n*, and we are actually given everything we need to find *d*. 

Remember, *d ≡ e<sup>-1</sup> (mod φ(n))* and *φ(n) = (p - 1)(q - 1)*. We are given *n* and *p*, so we can find *q*. Thus, we have everything we need to produce the plaintext.
```
#### TIME TO SHOW ME WHAT YOU GOT! ###
plaintext: 
```
It's **very** important to note here that the ciphertext provided to you is unique to your picoCTF account. Therefore, it will be slightly different for everyone. Make sure your decrypting your unique ciphertext and not the ciphertext I have here.

Here's a python script to do this encryption for us:
```python
from Crypto.Util.number import inverse

p = 153143042272527868798412612417204434156935146874282990942386694020462861918068684561281763577034706600608387699148071015194725533394126069826857182428660427818277378724977554365910231524827258160904493774748749088477328204812171935987088715261127321911849092207070653272176072509933245978935455542420691737433
c = 17712948302053968160337608808023765353713891487724504165710075800666176704275900270871131114252105275962867934935572601922131269231577652839874752278037120009042079114201440532529424282349775046830004126930931418790562922816147664822871476098418888441696782597264107603520215924140671864491508516555630119132820414262583115708142593728022851982531082194761937261873838830778405312620786370902097963783652483624611685252621820304116460797923537545175795133241570733730324869356742756474956593641308168807758853188030625975084213572477077655289967561799083034525042713829515144782123152608246868892673838596163063470464
e = 65537
n = 23952937352643527451379227516428377705004894508566304313177880191662177061878993798938496818120987817049538365206671401938265663712351239785237507341311858383628932183083145614696585411921662992078376103990806989257289472590902167457302888198293135333083734504191910953238278860923153746261500759411620299864395158783509535039259714359526738924736952759753503357614939203434092075676169179112452620687731670534906069845965633455748606649062394293289967059348143206600765820021392608270528856238306849191113241355842396325210132358046616312901337987464473799040762271876389031455051640937681745409057246190498795697239
q = n // p
totient = (p - 1) * (q - 1)
d = inverse(e, totient)
m = pow(c, d, n)
print(m)
```
Here is **my** message. Remember, yours will probably be different.
<details>
  <summary>Plaintext:</summary>
  14311663942709674867122208214901970650496788151239520971623411712977120545970596944152836477
</details>

Once you enter your unique plaintext message, the prompt tells you to convert the plaintext to hex, then to ascii. Here's some python code that can do that for us:
```python
from Crypto.Util.number import long_to_bytes

m = 14311663942709674867122208214901970650496788151239520971623411712977120545970596944152836477
print(long_to_bytes(m))
```

Remember, your flag will be unique to you, but it should follow the format below with the X's replaced with random characters.
<details>
  <summary>Flag:</summary>
  picoCTF{wA8_th4t$_ill3aGal..XXXXXXXXX}
</details>

[Return to Cryptography](https://github.com/sdvickers98/picoCTF-2019-Walkthrough/blob/master/cryptography/%230%20-%20Cryptography%20Home%20Page.md)

[Return to Homepage](https://github.com/sdvickers98/picoCTF-2019-Walkthrough)

