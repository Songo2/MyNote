# LangChain 框架入门与实战指南

创建时间：2026-05-24 00:54

编写:DEEPSEEK_API
标签:## 1. 什么是 LangChain  
LangChain 是一个用于开发由语言模型驱动的应用程序的框架。它提供标准化的接口、丰富的组件和预置链，帮助开发者将大语言模型（LLM）与外部数据源、工具、记忆等组合在一起，从而构建复杂的智能应用。  

### 1.1 核心理念  
- **链（Chain）**：将多个模型调用、数据处理步骤串联成可复用的序列。  
- **代理（Agent）**：让 LLM 自主决策使用哪些工具、按什么顺序执行，并观察结果，形成动态调用链。  
- **记忆（Memory）**：为多轮对话保留上下文状态。  
- **检索器（Retriever）**：将外部文档向量化并实现语义搜索，丰富模型的知识。  

### 1.2 适用场景  
- 聊天机器人（带历史记录、外部知识库）  
- 文档问答（PDF、数据库、网页内容问答）  
- 自动化工作流（邮件摘要、代码生成、数据分析）  
- 多步推理任务（结合搜索引擎、计算器、API 等工具）  

---

## 2. 环境搭建  

### 2.1 安装 LangChain  
```bash
pip install langchain
```
常用额外依赖：
```bash
pip install langchain-openai langchain-chroma langchainhub
pip install python-dotenv   # 管理环境变量
```

### 2.2 配置 API 密钥  
在项目根目录创建 `.env` 文件：
```
OPENAI_API_KEY=your_key_here
```
代码中加载：
```python
from dotenv import load_dotenv
load_dotenv()
```

---

## 3. 核心组件详解  

### 3.1 LLM 与聊天模型  

**基础 LLM**（输入文本，返回文本）：
```python
from langchain.llms import OpenAI
llm = OpenAI(temperature=0.7)
response = llm.invoke("用一句话解释人工智能")
```

**聊天模型**（输入消息列表，返回消息）：
```python
from langchain.chat_models import ChatOpenAI
from langchain.schema import HumanMessage

chat = ChatOpenAI(model="gpt-4o-mini", temperature=0.5)
msg = chat.invoke([HumanMessage(content="你好，请做自我介绍")])
print(msg.content)
```

### 3.2 提示模板  
使用模板保持输入结构一致，方便动态填充变量：
```python
from langchain.prompts import PromptTemplate

template = "将以下文本翻译成{target_language}：{text}"
prompt = PromptTemplate.from_template(template)

formatted = prompt.format(target_language="法语", text="你好，世界")
# -> "将以下文本翻译成法语：你好，世界"
```
**聊天模板**：
```python
from langchain.prompts import ChatPromptTemplate, SystemMessagePromptTemplate, HumanMessagePromptTemplate

system = SystemMessagePromptTemplate.from_template("你是一个专业的{role}。")
human = HumanMessagePromptTemplate.from_template("{input}")
chat_prompt = ChatPromptTemplate.from_messages([system, human])

messages = chat_prompt.format_messages(role="翻译专家", input="Hello world")
# [SystemMessage(content="你是一个专业的翻译专家。"), HumanMessage(content="Hello world")]
```

### 3.3 链（Chain）  
把组件串联，实现多步处理：
```python
from langchain.chains import LLMChain

chain = LLMChain(llm=llm, prompt=prompt)  # 使用前面定义的 prompt 和 llm
result = chain.run(target_language="日语", text="今天天气真好")
```
**更强大的 LCEL（LangChain 表达式语言）**：
```python
chain = prompt | llm   # 管道符组成可调用链
response = chain.invoke({"target_language": "日语", "text": "今天天气真好"})
```
LCEL 支持流式输出、异步调用，是推荐的链构建方式。

### 3.4 输出解析器  
让模型返回结构化数据（JSON、列表等）：
```python
from langchain.output_parsers import CommaSeparatedListOutputParser

parser = CommaSeparatedListOutputParser()
prompt = PromptTemplate(
    template="列出5个{category}的著名城市，用逗号分隔。\n{format_instructions}",
    input_variables=["category"],
    partial_variables={"format_instructions": parser.get_format_instructions()}
)
chain = prompt | llm | parser
result = chain.invoke({"category": "欧洲"})
# ['巴黎', '伦敦', '罗马', '柏林', '巴塞罗那']
```

### 3.5 记忆（Memory）  
为对话保留上下文：
```python
from langchain.memory import ConversationBufferMemory
from langchain.chains import ConversationChain

memory = ConversationBufferMemory(return_messages=True)
conversation = ConversationChain(llm=chat, memory=memory, verbose=True)

conversation.predict(input="我叫小明，我喜欢编程。")
conversation.predict(input="我叫什么名字？")  # 模型会回答"小明"
```

### 3.6 检索增强生成（RAG）  
**步骤拆解**：  
1. **加载文档**  
```python
from langchain.document_loaders import TextLoader
loader = TextLoader("knowledge.txt")
documents = loader.load()
```
2. **分割文档**  
```python
from langchain.text_splitter import RecursiveCharacterTextSplitter
text_splitter = RecursiveCharacterTextSplitter(chunk_size=500, chunk_overlap=50)
splits = text_splitter.split_documents(documents)
```
3. **向量化与存储**  
```python
from langchain.embeddings.openai import OpenAIEmbeddings
from langchain.vectorstores import Chroma

embeddings = OpenAIEmbeddings()
vectorstore = Chroma.from_documents(splits, embeddings)
retriever = vectorstore.as_retriever(search_kwargs={"k": 3})
```
4. **构建问答链**  
```python
from langchain.chains import RetrievalQA

qa_chain = RetrievalQA.from_chain_type(
    llm=llm,
    chain_type="stuff",
    retriever=retriever,
    return_source_documents=True
)
answer = qa_chain.invoke("请总结文件中的主要内容")
print(answer["result"])
# 可查看 answer["source_documents"] 获取出处
```

### 3.7 代理与工具  
代理 = LLM + 工具 + 决策循环，让模型动态调用外部功能。
```python
from langchain.agents import initialize_agent, Tool, AgentType
from langchain.tools import Tool
import requests

# 自定义工具：天气预报
def get_weather(city: str) -> str:
    # 示例用固定返回，实际改为 API 调用
    return f"{city}今天晴朗，25°C"

tools = [
    Tool(name="天气查询", func=get_weather, description="输入城市名获取天气信息"),
    Tool(name="计算器", func=eval, description="进行数学运算，输入表达式字符串")
]

agent = initialize_agent(
    tools, 
    chat, 
    agent=AgentType.CHAT_ZERO_SHOT_REACT_DESCRIPTION,
    verbose=True
)

agent.run("帮我查一下北京的天气，然后用计算器算一下123*456")
```
LangChain 已内置多种工具：搜索引擎（SerpAPI）、维基百科、Python REPL 等。

---

## 4. 使用最佳实践  

### 4.1 流式输出  
```python
for chunk in llm.stream("写一首关于夏天的诗"):
    print(chunk, end="", flush=True)
```
使用 `astream_events` 获得更丰富的事件流。

### 4.2 缓存降低成本  
```python
from langchain.cache import InMemoryCache
import langchain

langchain.llm_cache = InMemoryCache()
# 第二次相同请求会直接从缓存读取，不调用 API
```

### 4.3 回调监控  
```python
from langchain.callbacks import StdOutCallbackHandler

chain = prompt | llm
chain.invoke({"input": "hello"}, config={"callbacks": [StdOutCallbackHandler()]})
```
还可集成 LangSmith 等平台进行 trace 和调试。

### 4.4 结构化输出模式  
使用 `with_structured_output` 方法（需 chat 模型支持）直接输出 Pydantic 模型：
```python
from pydantic import BaseModel, Field

class Weather(BaseModel):
    city: str = Field(description="城市名")
    temperature: float = Field(description="温度（摄氏度）")

model_with_structure = ChatOpenAI(model="gpt-4o").with_structured_output(Weather)
result = model_with_structure.invoke("北京今天25度")
# Weather(city='北京', temperature=25.0)
```

### 4.5 注意版本迁移  
LangChain 更新较快，注意区分 `langchain`, `langchain-core`, `langchain-community` 等包。官方推荐用 LCEL 构建链，逐渐取代旧的 `LLMChain` 风格。

---

## 5. 实战项目：个人知识库问答系统  

### 5.1 项目结构  
```
knowledge_chatbot/
├── .env
├── main.py
├── data/               # 放 txt、pdf 等文档
└── vectordb/           # 持久化向量库
```

### 5.2 核心代码  
```python
import os
from dotenv import load_dotenv
from langchain.document_loaders import DirectoryLoader, TextLoader
from langchain.text_splitter import RecursiveCharacterTextSplitter
from langchain.embeddings.openai import OpenAIEmbeddings
from langchain.vectorstores import Chroma
from langchain.chat_models import ChatOpenAI
from langchain.chains import RetrievalQA

load_dotenv()

# 加载文档
loader = DirectoryLoader("data", glob="*.txt", loader_cls=TextLoader)
documents = loader.load()

# 分割
splitter = RecursiveCharacterTextSplitter(chunk_size=800, chunk_overlap=100)
docs = splitter.split_documents(documents)

# 向量化并持久化
embedding = OpenAIEmbeddings()
if not os.path.exists("vectordb"):
    vectordb = Chroma.from_documents(docs, embedding, persist_directory="vectordb")
    vectordb.persist()
else:
    vectordb = Chroma(persist_directory="vectordb", embedding_function=embedding)

# 问答链
qa = RetrievalQA.from_chain_type(
    llm=ChatOpenAI(model="gpt-4o-mini"),
    chain_type="stuff",
    retriever=vectordb.as_retriever(),
    return_source_documents=False
)

# 交互式问答
while True:
    query = input("你：")
    if query.lower() in ("exit", "quit"):
        break
    answer = qa.invoke(query)
    print(f"助手：{answer['result']}")
```

### 5.3 扩展方向  
- 增加 Web 界面（如 Streamlit 或 Gradio）  
- 支持多格式文档（PDF、Word、网页）  
- 加入对话记忆，形成多轮上下文  
- 用代理自动决定是否需要检索，或在检索不到时搜索网络  

---

## 6. 资源与参考  
- 官方文档：https://python.langchain.com  
- GitHub：https://github.com/langchain-ai/langchain  
- 教程：LangChain 官方 Cookbook、DeepLearning.AI 免费课程  

通过这个笔记，你应该能够搭建基础的 LangChain 应用，并理解其核心抽象。实践中遇到问题，建议查阅官方文档和社区讨论，紧跟版本更新。