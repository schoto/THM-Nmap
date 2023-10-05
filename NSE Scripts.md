<h2>Overview</h2>

The Nmap Scripting Engine (NSE) is an incredibly powerful addition to Nmap, extending its functionality quite considerably. 
NSE Scripts are written in the Lua programming language, and can be used to do a variety of things: from scanning for vulnerabilities, to automating exploits for them. 
The NSE is particularly useful for reconnaisance, however, it is well worth bearing in mind how extensive the script library is.

There are many categories available. Some useful categories include:

```safe```:- Won't affect the target

```intrusive```:- Not safe: likely to affect the target

```vuln```:- Scan for vulnerabilities

```exploit```:- Attempt to exploit a vulnerability

```auth```:- Attempt to bypass authentication for running services (e.g. Log into an FTP server anonymously)

```brute```:- Attempt to bruteforce credentials for running services

```discovery```:- Attempt to query running services for further information about the network (e.g. query an SNMP server).

**Questions / Answers**

What language are NSE scripts written in?

```LUA```

Which category of scripts would be a very bad idea to run in a production environment?

```intrusive```

**Working with the NSE**

In Task 3 we looked very briefly at the ```--script``` switch for activating NSE scripts from the ```vuln``` category using ```--script=vuln```. It should come as no surprise that the other categories work in exactly the same way. If the command ```--script=safe``` is run, then any applicable safe scripts will be run against the target (Note: only scripts which target an active service will be activated).

To run a specific script, we would use ```--script=<script-name>``` , e.g. ```--script=http-fileupload-exploiter```.

Multiple scripts can be run simultaneously in this fashion by separating them by a comma. For example: ```--script=smb-enum-users,smb-enum-shares```.

Some scripts require arguments (for example, credentials, if they're exploiting an authenticated vulnerability). These can be given with the ```--script-args Nmap switch```. An example of this would be with the ```http-put``` script (used to upload files using the PUT method). This takes two arguments: the URL to upload the file to, and the file's location on disk.  For example:

```
nmap -p 80 --script http-put --script-args http-put.url='/dav/shell.php',http-put.file='./shell.php'
```

Note that the arguments are separated by commas, and connected to the corresponding script with periods (i.e.  ```<script-name>.<argument>)```.

Nmap scripts come with built-in help menus, which can be accessed using nmap ```--script-help <script-name>```. This tends not to be as extensive as in the link given above, however, it can still be useful when working locally.


