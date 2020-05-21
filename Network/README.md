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
