# CE01
```
Download the file at https://ggcs-files.allyourbases.co/ce01.zip and solve the cipher to get the flag.

Note: The flag is in uppercase like THIS.
```
If we download this file, we see a lot of text.
```
IB EVMJGASVCJNM, C TRKTGIGRGIAB EIJNPV IT C OPGNAZ AQ PBEVMJGIBS KM YNIEN RBIGT AQ JWCIBGPHG CVP VPJWCEPZ YIGN EIJNPVGPHG, CEEAVZIBS GA C QIHPZ TMTGPO; GNP "RBIGT" OCM KP TIBSWP WPGGPVT (GNP OATG EAOOAB), JCIVT AQ WPGGPVT, GVIJWPGT AQ WPGGPVT, OIHGRVPT AQ GNP CKAXP, CBZ TA QAVGN. GNP VPEPIXPV ZPEIJNPVT GNP GPHG KM JPVQAVOIBS GNP IBXPVTP TRKTGIGRGIAB. GNP QWCS IT CTIOJWPTRKTGIGRGIAB
```
We can try multiple things on it, I found that cracking it with a substitution solver did the trick!
`https://www.guballa.de/substitution-solver`
Giving the output of:
```
IN CRYPTOGRAPHY, A SUBSTITUTION CIPHER IS A METHOD OF ENCRYPTING BY WHICH UNITS OF PLAINTEKT ARE REPLACED WITH CIPHERTEKT, ACCORDING TO A FIKED SYSTEM; THE "UNITS" MAY BE SINGLE LETTERS (THE MOST COMMON), PAIRS OF LETTERS, TRIPLETS OF LETTERS, MIKTURES OF THE ABOVE, AND SO FORTH. THE RECEIVER DECIPHERS THE TEKT BY PERFORMING THE INVERSE SUBSTITUTION. THE FLAG IS ASIMPLESUBSTITUTION
```
![Breaking the message](/images/CE01.png)

which gives us our flag!
Flag: ASIMPLESUBSTITUTION

# CE02
```
Download the file at https://ggcs-files.allyourbases.co/ce02.zip and solve the cipher to get the flag.

Note: The flag is in uppercase like THIS.
```
Again, we have a lot of text
```
RW LAHYCXPAJYQH, J LJNBJA LRYQNA, JUBX TWXFW JB LJNBJA'B LRYQNA, CQN BQROC LRYQNA, LJNBJA'B LXMN XA LJNBJA BQROC, RB XWN XO CQN BRVYUNBC JWM VXBC FRMNUH TWXFW NWLAHYCRXW CNLQWRZDNB. RC RB J CHYN XO BDKBCRCDCRXW LRYQNA RW FQRLQ NJLQ UNCCNA RW CQN YUJRWCNGC RB ANYUJLNM KH J UNCCNA BXVN ORGNM WDVKNA XO YXBRCRXWB MXFW CQN JUYQJKNC. OXA NGJVYUN, FRCQ J UNOC BQROC XO 3, M FXDUM KN ANYUJLNM KH J, N FXDUM KNLXVN K, JWM BX XW. CQN VNCQXM RB WJVNM JOCNA SDURDB LJNBJA, FQX DBNM RC RW QRB YAREJCN LXAANBYXWMNWLN. CQN OUJP RB LJNBJAAXCBCQNKAJRW.
```
This again just becomes trying multiple things until something works, I found that decrypting it with ROT13 or Caesar Cipher with key 9 worked and gave us our plaintext.
```
IN CRYPTOGRAPHY, A CAESAR CIPHER, ALSO KNOWN AS CAESAR'S CIPHER, THE SHIFT CIPHER, CAESAR'S CODE OR CAESAR SHIFT, IS ONE OF THE SIMPLEST AND MOST WIDELY KNOWN ENCRYPTION TECHNIQUES. IT IS A TYPE OF SUBSTITUTION CIPHER IN WHICH EACH LETTER IN THE PLAINTEXT IS REPLACED BY A LETTER SOME FIXED NUMBER OF POSITIONS DOWN THE ALPHABET. FOR EXAMPLE, WITH A LEFT SHIFT OF 3, D WOULD BE REPLACED BY A, E WOULD BECOME B, AND SO ON. THE METHOD IS NAMED AFTER JULIUS CAESAR, WHO USED IT IN HIS PRIVATE CORRESPONDENCE. THE FLAG IS CAESARROTSTHEBRAIN.
```
Giving us our flag!
Flag: CAESARROTSTHEBRAIN

# CE03
```
Download the file at https://ggcs-files.allyourbases.co/ce03.zip and solve the cipher to get the flag.

Note: The cipher is some form of AES encryption.
```
The briefing tells us it is AES encryption, and because we don't have an IV (initialization vector), we can assume this is AES in ECB mode.
We can see the ciphertext encoded in base16 or hexadecimal.
```
4870412d81d8af4b494c56462a4d684f24baee6f89627a995dfb6beccb404726e06ea8b99c9cbbe0b906ff5eec76ad602c85903f3e7f40156570cec56a19c244c3c69d9a00cbd4e9606288e1ea2e8b1f8bb1932d1ab67d0e9cb04de01adaac0a5e4558c90df8b519012d8d6a94a5c08e1d1dd81e07b8f2b6f87863290ad1c245530fa9894d9be8c8d2a1d8325a9bf1015180d3247130f170b3f5325c290f75b8eb2cf983443df33eedd6164c308674f21d6e47284983fc7132d056c1b34acc9c3d0bf62f9ea94e7f0cda7ab4d91d92089ccdcb1644f8390ddc27ef27f759870a53910a7407ea8c0896c73fd7841c2f75515512e0a6d4b912cd540b4c444c87a7
```
We are also given the key used, which is `iamakeykeykeykey` which makes decrypting this quite simple. 
I used CyberChef, a very useful tool for basic cryptography things.
`https://gchq.github.io/CyberChef/#recipe=AES_Decrypt(%7B'option':'UTF8','string':'iamakeykeykeykey'%7D,%7B'option':'Hex','string':''%7D,'ECB','Hex','Raw',%7B'option':'Hex','string':''%7D)&input=NDg3MDQxMmQ4MWQ4YWY0YjQ5NGM1NjQ2MmE0ZDY4NGYyNGJhZWU2Zjg5NjI3YTk5NWRmYjZiZWNjYjQwNDcyNmUwNmVhOGI5OWM5Y2JiZTBiOTA2ZmY1ZWVjNzZhZDYwMmM4NTkwM2YzZTdmNDAxNTY1NzBjZWM1NmExOWMyNDRjM2M2OWQ5YTAwY2JkNGU5NjA2Mjg4ZTFlYTJlOGIxZjhiYjE5MzJkMWFiNjdkMGU5Y2IwNGRlMDFhZGFhYzBhNWU0NTU4YzkwZGY4YjUxOTAxMmQ4ZDZhOTRhNWMwOGUxZDFkZDgxZTA3YjhmMmI2Zjg3ODYzMjkwYWQxYzI0NTUzMGZhOTg5NGQ5YmU4YzhkMmExZDgzMjVhOWJmMTAxNTE4MGQzMjQ3MTMwZjE3MGIzZjUzMjVjMjkwZjc1YjhlYjJjZjk4MzQ0M2RmMzNlZWRkNjE2NGMzMDg2NzRmMjFkNmU0NzI4NDk4M2ZjNzEzMmQwNTZjMWIzNGFjYzljM2QwYmY2MmY5ZWE5NGU3ZjBjZGE3YWI0ZDkxZDkyMDg5Y2NkY2IxNjQ0ZjgzOTBkZGMyN2VmMjdmNzU5ODcwYTUzOTEwYTc0MDdlYThjMDg5NmM3M2ZkNzg0MWMyZjc1NTE1NTEyZTBhNmQ0YjkxMmNkNTQwYjRjNDQ0Yzg3YTc`

![Decrypting the message](/images/CE03.png)

Which gave us our decrypted message, and our flag!
```
The Advanced Encryption Standard (AES), also known by its original name Rijndael, is a specification for the encryption of electronic data established by the U.S. National Institute of Standards and Technology (NIST) in 2001. The flag is: RijNdaelMe-9912
```
Flag: RijNdaelMe-9912

# CE04
```
Download the file at https://ggcs-files.allyourbases.co/ce04.zip and solve the cipher to get the flag.

Note: The flag is the encryption key used to encrypt the cipher.
```
Again, we have a lot of ciphertext.
```
Ulp Giysbssi ntpzsf wt e xptzcr cg iynrqdhwok lwpzopsumn eeph pm vwtyg s gsfjid zf abhssazgef Qostec nihvsft, fldev cb hii wptlsfg pj l veqkcfe. Me pmhzcmt e qzre ct dppjllhvopfxtn smpghjxfeigb.
```
And once again, it ended up being trying a bunch of things until it worked. 
This encryption turned out to be a Vigenere cipher, and the flag was the encryption key.
I used `https://www.guballa.de/vigenere-solver` to get the flag.

![Cracking the message](/images/CE04.png)

It decoded with the key `bellasooo`.
```
The Vigenere cipher is a method of encrypting alphabetic text by using a series of interwoven Caesar ciphers, based on the letters of a keyword. It employs a form of polyalphabetic substitution.
```
As said in the briefing, the flag was the encryption key, and therefore the flag is `bellasooo`

Flag: bellasooo
