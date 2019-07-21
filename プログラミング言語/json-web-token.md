## pythonで触る
```python
import jwt

key = 'secret'
payload = {
    'email': 'user@example.com',
}
encoded = jwt.encode(payload, key = key, algorithm='HS256')
print(encoded)
> b'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InVzZXJAZXhhbXBsZS5jb20ifQ.DXoyM6RiPLpg_lZmHfSWmYzORaEL0gD-5YJcHYQxNkk'
```  
byte型で帰ってくるらしいので↓
```python
print(encoded.decode("utf-8"))
> eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJlbWFpbCI6InVzZXJAZXhhbXBsZS5jb20ifQ.z0fgalndbQNB4wT138ZGJU7xYhZwJMRnJKjTYL25D7o
```  
文字列として扱うことができる
