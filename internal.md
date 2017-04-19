
# Internal

## Security

### level1:

For get method, add a token after the URL

### level2:

For post method or JSON,

validate: Exists(subTime) && Exists(token) && SHA256(subTime + key) == token && timediff(subTime, now()) <= TTL

key is a static string

### level3

(Not yet be done)

maybe key becomes dynamic: key = hash(post_data + time)

## APIs

### [lv1]	/Collection/printSTU/{token}

### [lv1]	/Collection/AddStu/{token}/{stu_id}

### [lv1]	/Collection/AddT/{token}/{test_id}/{problem_id}/{stu_id}

### [lv1]	/problem/getProbById/{problem_id}/{token = ''}

### [lv1]	/problem/getProbList/{offset = 0}/{token = ''}

### [lv1]	/file/l/{token = ''}

### [lv2]	/submit/xq

### [lv2]	/console	*//method: post json*

**action:	rank**

**action:	chart**

**action:	t1**

**action:	gt1**

**action:	grading**

**action:	rejudgeByPidAndStatus**

**action:	rejudgeByMDAndStatus**

**action:	addAllTest**

**action:	rank**

### [lv2]	/console/jsonp



----

* End

