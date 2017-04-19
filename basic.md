# File System

/-root

|----application	:	Main files (CI structure)

|----files		:	Files for download

|----probs		:	Problems file folder (each problem one directory, for problem folders' structure, see collection part)

|----static		:	JS and CSS files

|----tmp		:	Temporary files, 0777 (all submission and cache & log)

|----tools		:	Tools folder (Mars, ISE cmp tools, logisim)

----

# Database

## prob	[problem packet]

{id, title, view, lang, source, ac, submission, fileSize, cases, st, preg}

## status	[status packet]

{id, uid, pid, token, msg, dateTime, status, correct}

----

# Work Flow

1. submission request
2. authentication
3. job allocating
4. validation
5. judge
6. record submission
7. response

----

# Server

Recommended:

**Ubuntu 16.04**

**PHP 7.0.15**

**Apache 2.4.18**

**MySQL 14.14 Distrib 5.7.17**

**python2 2.7.12	python3 3.5.2**

