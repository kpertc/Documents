#python 

[Beautiful Soup 官网](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)

### Installation

beautifulsoup4

```
pip install beautifulsoup4

pip3 install beautifulsoup4
```

lxml

```
pip install lxml

pip3 install lxml
```

AJAX - Asynchronous JavaScript and XML

Parsing: interpret to Python

``` python
import requests

content = requests.get('https://i.snssdk.com/motor/car_page/v6/car_3d/config_v2?series_id=993&unity_platform=Android&preview_mode=1').json()

#print (content)

length = content['data']['body_size']['length']
width = content['data']['body_size']['width']
height = content['data']['body_size']['height']
wheel_base = content['data']['body_size']['wheel_base']

print(length)
print(width)
print(height)
print(wheel_base)
```
