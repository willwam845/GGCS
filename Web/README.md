# WE01

```
Access the site at https://ggcs-we01.allyourbases.co and see if you can find the flag in a common directory.
Hint: Think about places you could get a list of common directories to check for.
```

I decided to run dirb on the webpage to see if I could find anything.


![Dirb results](/images/WE01.png)

After a load of 403s, we can see 3 pages that don't yield a 403, which are index.html, soap and sample.
index.html simply gives the original page, so that was quite useless.
soap appears to be blank, so we skip it too.
However if we go to /sample, we can see a file called flag.txt, which we can then visit to get the flag.
https://ggcs-we01.allyourbases.co/sample/flag.txt
![Flag!](/images/WE01a.png)
Flag: bustING_direTORies_8918

# WE02
```
Access the site at https://ggcs-we02.allyourbases.co and see if you can find the flag on the site.
```

The website hints at viewing the source, so we do so

![Viewing the source](/images/WE02.png)

We can see an interesting Javascript page which is "/component---src-pages-else-js-b41975d5a1f03391fee1.js"
Therefore, we go visit it at https://ggcs-we02.allyourbases.co/component---src-pages-else-js-b41975d5a1f03391fee1.js

Visiting it, we can see the flag in the code.
![Flag!](/images/WE02a.png)
Flag: webPACkEd-AlRiGHT_7182

# WE03
```
Access the site at https://ggcs-we03.allyourbases.co and find a secret page which contains the flag.
```

Visiting the page, nothing seems to pop out at first, so I read the briefing again.
It mentions a secret page, so my initial thought is to go to robots.txt, as there are often secret pages there.
![robots.txt](/images/WE03.png)
As we can see, there is a hidden page called /61829201829023.html
Therefore, we can visit this page at https://ggcs-we03.allyourbases.co/61829201829023.html and see what we can find.
And as it says in the briefing, the flag is right there!
![Flag!](/images/WE03a.png)
Flag: NO_CrAwLing_Plz_0192

# WE04
```
Visit the news site at https://ggcs-we04.allyourbases.co and see if you can find a way to access the article without subscribing.
```

Nothing appears to pop out, so we look at the source code. 
![Source code](/images/WE04.png)
We can see that there is an interesting HTML comment:
```
<!--TODO: SEO is important to us, particularly Google's results are important!-->
```
The headline also hints at robots. 
If we do a quick google search for Google and robots, we can see something called Googlebot.
Right now the user agent is Applebot, so perhaps we need to change it to Googlebot?
And sure enough, the flag was indeed there when I changed the user agent.
![Changing the user agent](/images/WE04a.png)
![Flag!](/images/WE04b.png)
Flag: CrawlING-So-SlOwLY-8199

# WM01
```
Access the site at https://ggcs-wm01.allyourbases.co and find and then read the contents of the flag file to get the flag.
```
We appear to just have a linux file system, where we choose a path and then it will perform the ls command.
Perhaps then, we can use command injection, for example appending && and adding your command at the end.
![Command injection worked!](/images/WM01.png)
So then we can try and find this file.
After trying to find the file in many different directories, I decided to try and find it in the directory where we were, and sure enough, if we did `ls -a`, we could see a file called `.flag.txt`.
![Found the file!](/images/WM01a.png)
We then just do `cat .flag.txt` to get the flag!
![Flag!](/images/WM01b.png)
Flag: unSAFE_eXecution_42

# WM02
```
Visit the site at https://ggcs-wm02.allyourbases.co and find a way to log into the admin user without guessing a password.

Note: You can log in as a regular user with the username: linus and the password: torvalds
```
We can log in with these credentials, but it appears to just give us a blank page telling us we have logged in.
![Logged in?](/images/WM02.png)
