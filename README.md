# SessionBorderDiagAgent

v.1.0 单智能体框架+RAG

graph TD
    USER((用户原始输入)) --> ENHANCE[输入增强<br/>改写/意图识别/拆分]
    ENHANCE --> THINK[思考<br/>LLM 决策]
    THINK -- 需要信息 --> TOOL[工具调用]
    TOOL --> OBSERVE[观察<br/>工具结果]
    OBSERVE -- 继续分析 --> THINK
    THINK -- 已定位 --> ENDNODE((最终答案<br/>含引用))

    TOOL --> TOOLS[工具集合]
    TOOL --> RAG[RAG 知识库]

    TOOLS --> T1[SIP抓包]
    TOOLS --> T2[日志查询]
    TOOLS --> T3[配置比对]
    TOOLS --> T4[网络诊断]
    TOOLS --> T5[设备状态]

    RAG --> R1[SIP协议规范]
    RAG --> R2[错误码定义]
    RAG --> R3[历史案例]
    RAG --> R4[配置模板]





代码目录：
sip_fault_agent/
├── main.py                  # 入口：构建组件，输入增强，启动Agent
├── agent.py                 # 单Agent主循环 (ReAct)
├── input_enhancer.py        # 用户输入增强（口语转专业查询）
├── tools.py                 # 诊断工具模拟/真实接口
├── rag.py                   # 轻量RAG：向量检索、知识库构建
├── document_loader.py       # 文档加载与分块（Markdown + YAML头）
├── prompts.py               # 系统提示词、输入增强提示词
├── config.py                # 全局配置（API Key, 模型, 路径）
├── requirements.txt         # 依赖：openai, sentence-transformers, numpy, pyyaml
├── knowledge_base/          # 知识库原始文件
│   ├── rfc/
│   │   └── rfc3261.md
│   ├── product_docs/
│   │   ├── error_codes.md
│   │   └── sip_server_config.md
│   └── cases/
│       ├── case_001.md
│       └── case_002.md
└── tests/
    └── test_agent.py        # (可选) 单元测试
