# NE01 
```
There is a network service running on ggcs-ne01.allyourbases.co. Find it and connect to get the flag.

Note: The network service will identify itself with ID: ne01 when you connect to let you know you found the correct service.
```
Since we need to scan many ports, we can use a tool called `nmap` for this.
Running the command `nmap -Pn -T4 --min-rate=5000 -p- ggcs-ne01.allyourbases.co` will show all open ports.

![Open ports](/images/NE01.png)

We then try connecting to each of these ports, and see that when connecting to port 6166, we get the ID mentioned, and the flag!
`nc ggcs-ne01.allyourbases.co 6166`

![Correct port!](/images/NE01a.png)

Flag: hunTingPoRTS_7727

# NM01
```
Go to the target at ggcs-nm01.allyourbases.co port 6167 and connect.

Solve the questions in the time provided to get the flag.
```
Connecting to the server with `nc ggcs-nm01.allyourbases.co 6167`, we can see it presents us with a basic math problem, followed by an equals sign, presumambly to ask us to submit an answer. 
If I try to submit it normally, it will tell me I am too slow, so therefore we must use a script to submit answers, otherwise we won't be able to submit it on time.
![Too slow.](/images/NM01.png)

I decided to write this short script with the python library `pwntools`.
```
from pwn import *
p = remote("ggcs-nm01.allyourbases.co",6167)
for i in range(100):
  a = p.recvline()
  print(a)
  x = a.replace("=", "")
  b = eval(x)
  p.sendline(str(b))
```
Soon enough, we get an error in our code.
And we can see the flag printed in the error!
![Flag!](/images/NM01a.png)

Flag: QUiCKDraw_2323
