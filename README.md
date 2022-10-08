## CORRIDOR ROOM WALKTHROUGH --by konfushon

Today I'll be taking you through the corridor room (http://tryhackme.com/room/Corridor)
As always, we start with an nmap scan
 `nmap -sC -sV 10.10.162.207` 
We see that port 80 is open and nmap tells us that its running a python server.
On visting the website....we are greeted by just a single page with an image.
Viewing the page's  source code,we find out that there are seemingly more images...which appear to be hashed.

``In this challenge, you will explore potential IDOR vulnerabilities. Examine the URL endpoints you access as you navigate the website and note the hexadecimal values you find (they look an awful lot like a hash, don't they?). This could help you uncover website locations you were not expected to access`` 

At first I thought they were just random generated image links but looking at them closely, we see that they actually md5 hashes(md5 hashes are usually 32 characters in length). Trying to decrypt them gets us nowhere as we see that they are just numeric values.

I was stuck here for a while not knowing what to do with the information I had, but finally it hit me;
"The image links in the website take us somewhere,what if I generate my own links md5 hash them and try accessing that resultant url...(of course I had to cross-check my links to make sure that if my generated link matches with any of the already existing links in the webpage,I don't hit that endpoint as it will be useless [I already visited all the image links present in the webpage] )" 

With Python(not the snake) and the Internet on my side, I fumbled with a python script that allowed me to do exactly that.

I came to that thought because the room's description hinted that this room was about IDOR's and whatever I was about to do, was IDOR although with a twist.

Running the python script against the site, gives us two extra md5 hashes and testing the first one gives us the flag.

# The python script I used comes together with this README file in this repository