# SQL Injection + File Upload + Open Redirect — Online Voting System

**Repository:** https://github.com/itzzmerov/online-voting-system  
**GitHub Issue:** https://github.com/itzzmerov/online-voting-system/issues/3  
**Severity:** Critical (CVSS v3.1: 9.8)  
**CWE:** CWE-89, CWE-434, CWE-601  
**CVE:** Pending  
**Discovered:** 2026-06-19

## Vulnerability 1: SQL Injection

### `admin/candidates_delete.php`
```php
$id = $_POST['id'];
$sql = "DELETE FROM candidates WHERE id = '$id'";
```

### `admin/candidates_edit.php`
```php
$id=$_POST['id']; $name=$_POST['name']; $party=$_POST['party'];
$sql = "UPDATE candidates SET name='$name',party='$party' WHERE id='$id'";
```

## Vulnerability 2: Unrestricted File Upload

### `admin/candidates_add.php`
```php
move_uploaded_file($_FILES['photo']['tmp_name'], '../images/'.$filename);
```
No extension validation — PHP webshell uploadable → RCE.

## Vulnerability 3: Open Redirect

### `admin/config_save.php`
```php
$return = $_GET['return'];
header('location: '.$return);
```

**PoC:**
```
GET /admin/config_save.php?return=https://evil.com/phishing
```

## Fix
- Prepared statements for all SQL
- Validate file extension on upload
- Whitelist allowed redirect URLs
