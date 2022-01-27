# Personal Website Data Structure

A description of how I organize data for my website [jarkpark.net](https://jackpark.net).  Does not contain any source files.

I use Git to manage my website and the projects hosted on it, but I keep my website's repo private for security reasons.  This repo will illustrate how I organize directories and files to make the website work, as well as my develompent and deployment procedures.

# Directory Structure
```
/root
	index.html
	projects.html
	media.html
	blog.html
	contact.html
	/apps
	/css
	/js
	/resources
```
`root` contains the basic HTML pages for navigation (homepage, media page, etc.) as well as the website icon.  Nothing too special.

`apps` is where projects like the [Magic Spell Generator](https://gitgud.io/cold_quix/magic_spell_generator) and [Poker Tracker HTML](https://jackpark.net/apps/pokertracker.html) live.  Has a subdirectory for scripts which require CGI execution.

`css` and `js` contain CSS and JavaScript files, which are divided into common and page-specific files.

`resources` contains media that doesn't fit anywhere else, like the pictures on the front page and various PDFs.

Overall, it's a standard website structure, which should come as no surprise because my website is meant to be straightforward and simple.

# Development

Developing modules and apps for jackpark.net is simple: each project gets its own repo, and I manage them individually.  No module relies on data from other apps, and any database files are included in a subdirectory within that module (the [Magic Spell Generator](https://gitgud.io/cold_quix/magic_spell_generator) is a good example of this structure).

I do most of my development on a laptop.  In order to do local testing, I arrange modules within the website directory to mimic where they would appear when deployed to the webserver.  Cloning the website to test compatibility with each new project would result in a lot of unnecessary duplicate data.

This approach may sound a bit messy, but I have found it works perfectly fine for a one-man operation like me.  It would likely not suffice if I were developing a website as part of a larger team.

# Deployment

I develop on Windows, so deploying files to a webserver on a Linux VM requires some middleware: I use FileZilla to transfer files and PuTTY to enable remote SSH connections.  These programs are more secure than simply using a terminal's built-in SSH function because they allow me to authorize my connection with secure keys.  Anyone trying to gain access to my server would need to have my key, which is only stored in a couple private places.

Sometimes a program will require more effort than simply pushing files: the Magic Spell Generator [Python file](https://gitgud.io/cold_quix/magic_spell_generator/-/blob/master/spellgen.py) I had written in a Windows text editor had different carriage returns/line endings than what Linux expected, which caused problems.  In this case, I used PuTTY to manually create files on the Linux server in a command terminal, then manually paste in the contents of the source file.  This saved the text in a Linux-friendly format.

A bit of a hassle, but the additional control I have over individual files is worth it.

# Security

Web security is broadly governed by two ideas:
- Don't store anything critical.
- Don't give users/admins any more privileges than they need.

I am happy to say that nothing sensitive is stored on jackpark.net, which makes it a low value target.  My website also doesn't get much traffic, so there is little risk of it becoming DDoS'd or swamped by bot traffic.

Given how the site is configured, it is necessary for me to have root access to the Linux VM that it runs on.  This presents a danger because anyone who infiltrated the site would also have root access - but as I mentioned earlier, I use private keys to log on instead of usernames and passwords.  This means any hacker would first need to acquire my keys, which is impossible.
