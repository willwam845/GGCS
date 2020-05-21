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
