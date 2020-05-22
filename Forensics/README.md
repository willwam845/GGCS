# FE01
```
Download the file at https://ggcs-files.allyourbases.co/fe01.zip and find a way to extract the flag using the provided word list.
```
We get a wordlist and a zip.
To crack this we can use the tool `fcrackzip`
`fcrackzip -v -u -D -p wordlist.txt flag.zip`
![Password cracked!](/images/FE01.png)


Resulting in us finding the password of "digital"
We can then unzip the zip file with this password to get flag.txt and read the flag.

Flag: z1P-Cr4CK-0910

# FE02 
```
Download the file at https://ggcs-files.allyourbases.co/fe02.zip and see if you can recover the redacted document to get the flag.
```
If we try to copy all the text from the PDF, it appears to ignore the fact that it is covered.
Therefore, we can just copy the text into a file and get the flag.
![Copying it out](/images/FE02.png)
![Flag got.](/images/FE02a.png)

Flag: cAnYOuReALLYSEEme-2322

# FE03
```
Download the file at https://ggcs-files.allyourbases.co/fe03.zip and find a way to retrieve the flag from the gif.
```
Nothing seemed to pop out at first, so I ran strings on the gif.

![Interesting strings.](/images/FE03.png)

There appears to be something else inside this gif, as this did not look like something a gif would have. 
So, I put into good old CyberChef, and tried to extract any files.
![ooo an ELF](/images/FE03a.png)

We can see there is an ELF, so I extracted it and ran it.
And the flag was right there.

![Flag got!](/images/FE03b.png)

Flag: EMbEddedFiLEz_0819

# FE04
```
Download the file at https://ggcs-files.allyourbases.co/fe04.zip and find a way to recover the flag from the corrupted file.
```
The briefing says the file is corrupted, and by running strings on the file, I can make an educated guess that this is an ELF file.
However, the header of the file appears to be missing if we view it in `ghex`.
![Missing header](/images/FE04.png)

Therefore, we must add it to patch it.
![Patching](/images/FE04a.png)

We then simply run the ELF file to get the flag!

![Flag!](/images/FE04b.png)

Flag: DoNTLosEYOURHeAD-1181

# FE01
```
Download the file at https://ggcs-files.allyourbases.co/fm01.zip and use the included word list to extract the flag.
```
This time, using `fcrackzip` with the zip like we did last time doesn't appear to find a password.
![Hmmm... nothing...](/images/FM01.png)

There appears to be a new file called `policy.txt`
```
Note: All employees MUST use passwords that include at least one capital and one digit.
```
So the password probably had to comply to this rule.
We can use `john` to mangle the wordlist.
`john --wordlist=wordlist.txt --stdout --rules:Single > newwords.txt`
And then running `fcrackzip` with these new words yields the password `Cartoon4`
![Password found!](/images/FM01a.png)

We then use this password to unzip the file and get the flag.
Flag: mangLINg-w0RDs-62517

# FM02
```
Download the file at https://ggcs-files.allyourbases.co/fm02.zip and find a way to recover the flag from the provided images.
```
The first image appears to be a QR code, which we can scan to get the following message:
```
black and white images are very binary...
```
The mention of binary made me think, however this challenge ended up being very guessy. 
The solution was to bitwise XOR the 2 images. 
The output image was then a QR code you could scan and get the flag.
`convert 1.png 2.png -fx "(((255*u)&(255*(1-v)))|((255*(1-u))&(255*v)))/255" img_out`
We can then scan the `img_out` file to get the flag.

Flag: xOROROR-91822
