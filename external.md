# External

## Submission

### /submit

| post_item | type    | note            |
| --------- | ------- | --------------- |
| token     | string  | authentication  |
| prob      | integer | problem id      |
| code      | file    | the upload file |

response: json{status(int),result(enum)}

### /submit/xq

| json_item                                | type   | note           |
| ---------------------------------------- | ------ | -------------- |
| \['xqueue_body'\]\['token'\]             | string | authentication |
| \['xqueue_body'\]\['student_info'\]      | json   |                |
| \['xqueue_body'\]\['student_info'\]['submission_time'] | YmdHis |                |
| \['xqueue_body'\]\['student_info'\]['anonymous_student_id'] | string | student id     |
| \['xqueue_body'\]\['grader_payload'\]    | json   | action info    |
| ['xqueue_files']                         | json   | the file urls  |

**Example:**

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
**response:** json{correct(bool),score(float),msg(string)}

**Special statement of action info:**	the function of grader payload

1. {'p'=[problem_id], 't'='prob'}//submit a problem solution
2. {'p'=[test_id], 't'='test'}//submit a exam problem solution
3. {'p'=[problem_id], 't'='down'}//download the last solution of a problem (if exists)
4. {'p'=[test_id], 't'='downT'}//download the last solution of a exam problem
5. {'p'=[problem_id], 't'='queryP'}//query the last score of a problem
6. {'p'=[exam_id], 't'='query'}//query the exam status (pass//fail)
7. {'p'=[file_id], 't'='file'}//download a specific file
8. {'p'=[test_ids], 't'='queryT'}//download the specific exam problem descriptions by a list (split by ',')

## Problems

### /problem/getProbById/{problem_id}/{token = ''}

**Fail:** response = json{status(int), msg(string)}

**Success:** response = json{status(int), html(long text), [problem packet]}

### /problem/getProbList/{offset = 0}/{token = ''}

**Fail:** response = json{status(int), msg(string)}

**Success:** response = json{status(int), count(int), array of [problem packet]}

## Status

### /status/{offset = 0}

**Fail:** response = json{status(int), msg(string)}

**Success:** response = json{status(int), count(int), array of [status packet]}

