#从零学习爬虫

import urllib.request
#使用urllib.request.uelopen打开网址
#urlopen里面有三个参数：网址、post请求携带的参数例如登录名以及秘密、请求超时时间
#urlopen默认是GET请求，传入参数时就变为post请求了
response = urllib.request.urlopen('http://www.baidu.com')
#打印抓取到的数据
print(response.read().decode('utf-8'))
#这里返回的是网页的源码
#——————————————抓取HTTP或手机时————————————————————
from urllib import request,parse
import ssl#因为网址用的HTTPS，需导入ssl库
#使用 ssl 未经验证的上下文
context = ssl._create_unverified_context()
url = 'https://biihu.cc//account/ajax/login_process/'
headers = {
    #假装自己是浏览器
    'User-Agent':' Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36',
}
#请求时需要携带的数据：账户及其密码，这个可由finddle查看需要提交什么
dict = {
    'return_url':'https://biihu.cc/',
    'user_name':'xiaoshuaib@gmail.com',
    'password':'123456789',
    '_post_type':'ajax',
}
#将携带的数据进行编码在转换成bytes
data = bytes(parse.urlencode(dict),'utf-8')
#进行POST请求
req = request.Request(url,data=data,headers=headers,method='POST')
response = request.urlopen(req,context=context)
print(response.read().decode('utf-8'))


#————————requests库——————————————————————————————————


import requests
#GET请求
r = requests.get('https://api.github.com/events')
r
#post请求
r = requests.post('https://httpbin.org/post', data = {'key':'value'})
#其他Http请求
r = requests.put('https://httpbin.org/put', data = {'key':'value'})
r = requests.delete('https://httpbin.org/delete')
r = requests.head('https://httpbin.org/get')
r = requests.options('https://httpbin.org/get')
#——————GET请求携带参数————————————————————————

#使get请求携带参数，直接使用params解析携带的参数
payload = {'key1': 'value1', 'key2': 'value2'}
r = requests.get('https://httpbin.org/get', params=payload)
#——————假装自己时游览器————————————————————————
url = 'https://api.github.com/some/endpoint'
headers = {'user-agent': 'my-app/0.0.1'}
r = requests.get(url, headers=headers)
#————————获取服务器响应文本内容————————
#文本内容text
import requests
r = requests.get('https://api.github.com/events')
r.text
r.encoding
#————————————获取字节响应内容————————————
#字节响应内容：content
r.content
#————————获取响应码——————————————————
#响应码status_code
r = requests.get('https://httpbin.org/get')
r.status_code
#————————————获取响应头————————————————
r.headers
#——————————获取Json内容——————————————————
import requests
r = requests.get('https://api.github.com/events')
r.json()
#——————————获取 socket 流响应内容——————————
r = requests.get('https://api.github.com/events', stream=True)
r.raw
r.raw.read(10)



#——————————POST请求————————————————————
payload_tuples = [('key1', 'value1'), ('key1', 'value2')]
#携带参数不需像get使用params解析
r1 = requests.post('https://httpbin.org/post', data=payload_tuples)
payload_dict = {'key1': ['value1', 'value2']}
r2 = requests.post('https://httpbin.org/post', data=payload_dict)
print(r1.text)
r1.text == r2.text
#————————————————请求的时候用 json 作为参数————————————
url = 'https://api.github.com/some/endpoint'
payload = {'some': 'data'}
r = requests.post(url, json=payload)
#——————————上传文件————————————
url = 'https://httpbin.org/post'
files = {'file': open('report.xls', 'rb')}
r = requests.post(url, files=files)
r.text
#——————————获取cookies信息————————
url = 'http://example.com/some/cookie/setting/url'
r = requests.get(url)
r.cookies['example_cookie_name']
#——————————发送cookies消息————————————————————————
url = 'https://httpbin.org/cookies'
cookies = dict(cookies_are='working')
r = requests.get(url, cookies=cookies)
r.text
#——————————设置超时————————————
requests.get('https://github.com/', timeout=0.001)


#————————使用正则表达式来过滤我们需要的数据————————————————

