#data  #web-dev 

Requests → HTTP request
Parse information → Beautiful Soup [[Beautifulsoup - Web Scraping]]

[httpbin.org](https://httpbin.org/#/)

### Get
``` python
import requests

r = requests.get(" address ")
# r stand for response

r = requests.get(" address ", timeout=3)
# without timeout, requests will try forever
# watchout delay API
```

``` python
r.text -> unicode

# get content
r.content -> byte
# download the image
with open('xxx.png', 'wb') as f:
	f.write(r.content)

r.status_code # 200 -> ok
r.ok # -> boolean of connection 200, 300 True

r.header
r.headers.get('content-disposition')
#attachment; filename="image.png"; filename*=UTF-8''image.png
```

``` python
payload = {'page': 2, 'count': 25}
r = requests.get('https://httpbin.org/get', params = payload)
# set as params, instead of settring manually
r.url # ->  https://httpbin.org/get?page=2&count=25
```

##### Auth authentication
```python
r = requests.get('https://httpbin.org/basic-auth/username/password', auth = ('username', 'password')))

'''
return ->
{
  "authenticated": true, 
  "user": "username"
}
'''

```

### Post 
```python

# form authentication
payload = {'username': '_username_', 'password': 'password'}
r = requests.post('https://httpbin.org/post', data = payload)

# return object as json
python_dict = r.json()
python_dict['form']

```