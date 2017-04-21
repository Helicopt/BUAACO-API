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

1. submission request [/submit/xq or /submit]

   When the server receives a request, it firstly trim it (delete invalid characters), then turn to authentication.

2. authentication [/submit/xq or /submit]

   Use LV1 or LV2 method to authenticate the request, reject invalid requests.

3. job allocating [/submit/xq or /submit]

   According to the submission's author's id, the request will be delivered to the other server or just be judged locally.

4. validation  [model: subm.php]

   Before judging, the server will check the problem id or code type, in order to ensure that the submission is all right.

   For example, maybe the submission refers a wrong problem id, maybe the code is not suitable with the problem type, or, more seriously, the code contains hostile commands.

5. judge  [model: subm.php]

   For Verilog code, run command line 

   ```colab-wrapper _judge target_dir mem_file testbench.v submit.v output_file```

   For Logisim code design, run command 

   ```java -Djava.awt.headless=true -jar logisim.jar tester.circ -tty table ```

   ```-sub origin.circ submit.circ > outfile```

   For MARS code, run command

   ```java -Djava.awt.headless=true -jar mars.jar mc CompactDataAtZero 100000 submit.asm > outfile < infile```

   For all code, the server provides a standard comparing method to judge the result, and only when output is exactly the same as the answer will it gives a 'correct' response.

   Meanwhile, there are two special judge method, for Verilog and Logisim respectively.

   ```colab-wrapper judge outfile ansfile```

   ```python logi_cmp.py outfile ansfile ```

   These methods will consider more detail and finally give out the score.

6. record submission  [model: subm.php]

   After judgement, we will record the score, save the code, and update the database.

7. response [/submit/xq or /submit]

   Write back the result and inform the problem solver.

----

# Server

Recommended:

**Ubuntu 16.04**

**PHP 7.0.15**

**Apache 2.4.18**

**MySQL 14.14 Distrib 5.7.17**

**python2 2.7.12	python3 3.5.2**

----

* End