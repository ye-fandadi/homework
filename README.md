🤖 协作型智能 Agent 系统
本项目基于 LangChain 框架构建了一个具备多功能工具调用能力的协作型智能 Agent 系统，支持知识库问答、实时天气查询、自定义数据分析等任务，并通过 FastAPI 对外提供 RESTful API 服务接口，具备可扩展性与实用价值。

1. 🌟 项目背景与目标
本系统旨在打造一个多功能智能 Agent，具备以下能力：

理解用户自然语言意图；

调用知识库回答项目相关问题；

连接外部 API（如天气服务）；

执行自定义本地计算任务；

维持上下文记忆，实现多轮对话；

以 API 接口形式部署运行。

未来可扩展为多个协作 Agent 组成的系统，如信息检索 Agent、数据分析 Agent 等，形成模块化智能体协同工作平台。

2. 🛠 技术栈
模块	技术
智能体框架	LangChain
语言模型	DeepSeek Chat（通过 langchain_deepseek）
向量数据库	FAISS
嵌入模型	HuggingFace Sentence Transformers
文档加载	PyPDFLoader
Web 服务	FastAPI
环境变量管理	python-dotenv
网络请求工具	requests
数据分析	pandas
依赖管理	requirements.txt
版本控制	Git + GitHub

3. 🔧 系统功能与工具
3.1 知识库工具（KnowledgeBaseQueryTool）
功能：支持从本地 PDF 文档中回答用户问题。

技术流程：

使用 PyPDFLoader 加载文档；

使用 RecursiveCharacterTextSplitter 分块；

通过 HuggingFaceEmbeddings 转换为向量；

存入 FAISS 并通过 RetrievalQA 实现语义搜索问答；

示例：

输入：项目文档中 LangChain 的介绍是什么？

返回：从 PDF 文档中提取相关段落并回答。

3.2 天气查询工具（WeatherQueryTool）
功能：调用 OpenWeatherMap API 查询指定城市天气。

实现：使用 requests 向 OpenWeather API 发起请求，解析 JSON 响应。

示例：

输入：北京今天天气如何？

返回：天气描述、温度、湿度、风速等。

3.3 数据分析工具（DataAnalysisAndSortTool）
功能：对用户提供的数据进行排序与统计分析。

实现：

接收字符串格式的数据（如 "5, 8, 3"）；

解析后调用 sorted() 和 pandas 进行处理；

示例：

输入：请对数据 12, 5, 8, 3, 20 进行降序排列并计算平均值

返回：排序结果 + 均值/中位数/标准差等。

4. 🚀 快速启动
4.1 克隆项目
bash
复制
编辑
git clone https://github.com/<你的用户名>/collaborative-agent-system.git
cd collaborative-agent-system
4.2 安装依赖
bash
复制
编辑
python -m venv venv
# Windows
.\venv\Scripts\activate
# macOS/Linux
source venv/bin/activate

pip install -r requirements.txt
如果报错，可尝试：

bash
复制
编辑
pip install faiss-cpu pypdf
4.3 添加环境变量
在项目根目录创建 .env 文件：

env
复制
编辑
DEEPSEEK_API_KEY=your_deepseek_api_key_here
OPENWEATHER_API_KEY=your_openweather_api_key_here
4.4 添加知识库文档
请将你的 PDF 文档放在项目的 docs/ 目录下，命名为：

bash
复制
编辑
docs/the_history_of_ship.pdf
4.5 启动服务（app.py）
bash
复制
编辑
python app.py
5. 🧪 测试 API 接口
接口地址：

bash
复制
编辑
POST http://localhost:8000/chat
Content-Type: application/json
Body: {"query": "你的问题"}
示例请求：
查询天气：

curl -X POST http://localhost:8000/chat \
-H "Content-Type: application/json" \
-d '{"query": "上海天气如何？"}'

知识库问答：

curl -X POST http://localhost:8000/chat \
-H "Content-Type: application/json" \
-d '{"query": "轮船是何时出现的？？"}'
6. 🤝 合作与分工
姓名	主要负责内容
庄鹏程	系统整体设计，知识库工具构建，LangChain 集成，FastAPI 服务部署，README 编写
李思远	工具开发（天气 + 数据分析），Agent 调试，代码测试，文档补充，Git 协作

🙋 李思远的反思
深入理解了 Agent 的核心结构（LLM、工具、记忆、链）；

学会了 LangChain 工具调用机制；

遇到过 PDF 处理效果不佳的问题，后通过调整 chunk_size 解决；

部署 API 时，dotenv 的加载和路径问题曾卡住，后规范处理。

🙋 庄鹏程的反思
掌握了将天气 API 集成为 Agent 工具；

熟悉了自定义工具的数据处理逻辑与用户输入解析；

遇到 curl JSON 构造复杂问题，逐步学会不同终端格式；

合作开发中通过 Git 高效协同，解决了冲突合并问题。

7. 📌 附录（推荐）
7.1 目录结构示意：
bash
复制
编辑
collaborative-agent-system/
├── app.py
├── docs/
│   └── the_history_of_ship.pdf
├── .env
├── requirements.txt
├── README.md
8. 🔮 展望与扩展方向
增加多 Agent 协作机制（如 Planner + Tool Executor 分离）；

引入 LangGraph 构建更复杂的状态驱动智能体；

接入更多 API 工具（如股票查询、翻译等）；

构建前端 Web UI 实现自然语言界面对话；

支持用户动态上传知识库文档并自动生成索引。
