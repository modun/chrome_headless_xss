# **基于Chorme headless的xss检测**
## 源码及使用方法
Mac os 安装 chrome-canary：
```
brew install Caskroom/versions/google-chrome-canary
```
启动chrome远程调试：
```
chrome-canary --remote-debugging-port=9222 --headless -remote-debugging-address=0.0.0.0 --disable-xss-auditor --no-sandbox --disable-web-security
```
centos7：
安装chrome
```
$ vi /etc/yum.repos.d/google-chrome.repo
```
写入如下内容：
```
[google-chrome]
name=google-chrome
baseurl=http://dl.google.com/linux/chrome/rpm/stable/$basearch
enabled=1
gpgcheck=1
gpgkey=https://dl.google.com/linux/linux_signing_key.pub
```
然后
```
$ sudo yum install google-chrome-stable
```
后台启动chrome-stable
```
nohup google-chrome-stable --disable-gpu --remote-debugging-port=9222 --headless -remote-debugging-address=0.0.0.0 --disable-xss-auditor --no-sandbox --disable-web-security > chromeheadless.out 2>&1 & 
```
chrome_headless_xss
```
# tmp_url为添加payload的url，如果是post请求则为原始url
chrome_headless_drive = ChromeHeadLess(url=tmp_url,
ip="127.0.0.1",
port="9222",
cookie="",
post="",
auth="",
payloads= payload
#添加监听弹窗内容
check_message = "you_alert_message")
scan_result = chrome_headless_drive.run()
```
scan_result结果：
```
# level 3 代表触发了Page.javascriptDialogOpening事件
{'url': u'http://xss.php', 'vul': 'xss', 'post': '', 'method': u'GET', 'level': '3'}
# level 2 代表dom树的节点包含了我们自定义的<webscan></webscan>标签
{'url': u'http://xss.php', 'vul': 'xss', 'post': '', 'method': u'GET', 'level': '2'}
# level 1 代表渲染后的nodeValue包含我们的payload
{'url': u'http://xss.php', 'vul': 'xss', 'post': u'id1=1&id2=2test_test', 'method': u'POST', 'level': '1'}
```
源码链接：
```
https://github.com/neverlovelynn/chrome_headless_xss/
```

