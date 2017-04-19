# BUAACO Testing Platform API#

## File System##

/-root

|----application	:	Main files (CI structure)

|----files		:	Files for download

|----probs		:	Problems file folder (each problem one directory, for problem folders' structure, see collection part)

|----static		:	JS and CSS files

|----tmp		:	Temporary files, 0777 (all submission and cache & log)

|----tools		:	Tools folder (Mars, ISE cmp tools, logisim)

----

## Database##

### prob	[problem packet]###

{id, title, view, lang, source, ac, submission, fileSize, cases, st, preg}

### status	[status packet]###

{id, uid, pid, token, msg, dateTime, status, correct}

----

## Work Flow##

1. submission request
2. authentication
3. job allocating
4. validation
5. judge
6. record submission
7. response

----

## External##

### Submission###

**/submit**

| post_item | type    | note            |
| --------- | ------- | --------------- |
| token     | string  | authentication  |
| prob      | integer | problem id      |
| code      | file    | the upload file |

response: json{status(int),result(enum)}

**/submit/xq**

| json_item                                | type   | note           |
| ---------------------------------------- | ------ | -------------- |
| \['xqueue_body'\]\['token'\]             | string | authentication |
| \['xqueue_body'\]\['student_info'\]      | json   |                |
| \['xqueue_body'\]\['student_info'\]['submission_time'] | YmdHis |                |
| \['xqueue_body'\]\['student_info'\]['anonymous_student_id'] | string | student id     |
| \['xqueue_body'\]\['grader_payload'\]    | json   | action info    |
| ['xqueue_files']                         | json   | the file urls  |

Example:

```json
{
  'xqueue_files':
  	{"SRLatch.circ":"http://files.mooc.buaa.edu.cn/problems/BUAA+B3I062410+2016_T1/co-queue/3f82686a36994a6e90106482cd14a951/SRLatch.circ"},
  'xqueue_body':
  	{'token':'abcdefghijklmn',
     'grader_payload':{'p':'123','t':'test'},
     'student_info':{'anonymous_student_id':'14060000','submission_time':'20160808080808'},
     'student_response':''
    }
}
```
response: json{correct(bool),score(float),msg(string)}

Special statement of action info:	the function of grader payload

1. {'p'=[problem_id], 't'='prob'}//submit a problem solution
2. {'p'=[test_id], 't'='test'}//submit a exam problem solution
3. {'p'=[problem_id], 't'='down'}//download the last solution of a problem (if exists)
4. {'p'=[test_id], 't'='downT'}//download the last solution of a exam problem
5. {'p'=[problem_id], 't'='queryP'}//query the last score of a problem
6. {'p'=[exam_id], 't'='query'}//query the exam status (pass//fail)
7. {'p'=[file_id], 't'='file'}//download a specific file
8. {'p'=[test_ids], 't'='queryT'}//download the specific exam problem descriptions by a list (split by ',')

### Problems###

**/problem/getProbById/{problem_id}/{token = ''}**

Fail: response=json{status(int), msg(string)}

Success: response=json{status(int), html(long text), [problem packet]}

**/problem/getProbList/{offset = 0}/{token = ''}**

Fail: response=json{status(int), msg(string)}

Success: response=json{status(int), count(int), array of [problem packet]}

### Status###

**/status/{offset = 0}**

Fail: response=json{status(int), msg(string)}

Success: response=json{status(int), count(int), array of [status packet]}

----

## Internal##

### Security

#### level1:

For get method, add a token after the URL

#### level2:

For post method or JSON,

validate: Exists(subTime) && Exists(token) && SHA256(subTime + key) == token && timediff(subTime, now()) <= TTL

key is a static string

#### level3

(Not yet be done)

maybe key becomes dynamic: key = hash(post_data + time)

### APIs

#### [lv1]	/Collection/printSTU/{token}

#### [lv1]	/Collection/AddStu/{token}/{stu_id}

#### [lv1]	/Collection/AddT/{token}/{test_id}/{problem_id}/{stu_id}

#### [lv1]	/problem/getProbById/{problem_id}/{token = ''}

#### [lv1]	/problem/getProbList/{offset = 0}/{token = ''}

#### [lv1]	/file/l/{token = ''}

#### [lv2]	/submit/xq

#### [lv2]	/console	*//method: post json*

**action:	rank**

**action:	chart**

**action:	t1**

**action:	gt1**

**action:	grading**

**action:	rejudgeByPidAndStatus**

**action:	rejudgeByMDAndStatus**

**action:	addAllTest**

**action:	rank**

#### [lv2]	/console/jsonp

----

## Server##

Recommended:

Ubuntu 16.04

PHP 7.0.15

Apache 2.4.18

MySQL 14.14 Distrib 5.7.17

python2 2.7.12	python3 3.5.2



----