OpenAI在python里推出了openai开发库,在openai库里面我们一般常用OpenAI这个类

```python
from openai import OpenAI

client=OpenAI(
	api_key="我的密钥",
	base_url="AI模型的网址")
```
# OpenAI类
## api_key

调用AI的API的密钥,用于证明自己的用户身份,这个是必须填的

## base_url

AI的API地址,不填的话会是OpenAI的网址,需要调用其他AI的话必须填

## timeout

超时时间,单位为秒,超过时间就不调用了返回超时,不填则无限制

## max_retries

最大重试次数,如果超时就重试

# Completions类