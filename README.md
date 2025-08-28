# V2EX 论坛搜索插件
[English](README.en.md) | **中文**

**作者:** frederick  
**版本:** 0.0.1  
**类型:** Dify 工具插件  

## 插件描述

V2EX 论坛搜索插件是一个专为 Dify 平台设计的工具插件，可以帮助用户搜索和获取 V2EX 论坛的各种内容，包括热门主题、最新主题、节点信息和用户资料。该插件通过 V2EX 的公开 API 提供服务，无需任何认证即可使用。

## 主要功能

- 🔥 获取 V2EX 热门主题
- 🆕 获取 V2EX 最新主题  
- 📋 查询节点详细信息
- 👤 查询用户个人资料
- 🔍 支持关键词过滤搜索

## 分步设置说明

### 1. 环境要求

- Python 3.12+
- Dify 平台环境
- 网络连接（用于访问 V2EX API）

### 2. 安装依赖

```bash
pip install -r requirements.txt
```

### 3. 本地调试配置

1. 复制环境变量配置文件：
   ```bash
   cp .env.example .env
   ```

2. 编辑 `.env` 文件，配置以下变量：
   ```
   INSTALL_METHOD=remote
   REMOTE_INSTALL_URL=debug.dify.ai:5003  # 或您的 Dify 实例地址
   REMOTE_INSTALL_KEY=your_debug_key_here  # 从 Dify 插件管理页面获取
   ```

### 4. 启动插件进行调试

```bash
python -m main
```

### 5. 在 Dify 中安装插件

1. 在 Dify 插件管理页面上传 `plugin.difypkg` 文件
2. 或者使用调试模式直接连接本地运行的插件

## 详细使用说明

### 基本用法

插件提供一个名为 "V2EX内容搜索" 的工具，包含以下参数：

#### 1. 搜索类型 (search_type) - 必需
- **hot_topics**: 热门主题 - 获取当前热门讨论的主题
- **latest_topics**: 最新主题 - 获取最新发布的主题
- **node_info**: 节点信息 - 获取指定节点的详细信息
- **user_info**: 用户信息 - 获取指定用户的个人资料

#### 2. 搜索关键词 (search_query) - 可选
- 对于热门/最新主题：可以输入关键词进行内容过滤
- 对于节点信息：输入节点名称（如：python、javascript、apple）
- 对于用户信息：输入用户名或用户ID

#### 3. 结果限制 (limit) - 可选
- 设置返回结果的最大数量
- 默认值：10
- 范围：1-50

### 使用示例

#### 获取热门主题
```
搜索类型：hot_topics
搜索关键词：（留空获取全部，或输入"python"等关键词进行过滤）
结果限制：10
```

#### 查询节点信息
```
搜索类型：node_info
搜索关键词：python
结果限制：（不适用）
```

#### 查询用户信息
```
搜索类型：user_info
搜索关键词：Livid
结果限制：（不适用）
```

### 返回数据格式

插件会返回结构化的 JSON 数据，包含：
- 主题：标题、内容、链接、回复数、作者、节点信息等
- 节点：名称、描述、主题数量、链接等
- 用户：用户名、签名、简介、社交媒体链接等

## API 和认证要求

### V2EX API 信息
- **API 基础地址**: `https://www.v2ex.com/api`
- **认证要求**: 无需认证，V2EX API 完全公开
- **频率限制**: 每小时每IP最多120次请求
- **缓存**: 支持 CDN 缓存，重复请求不消耗配额

### 无需配置的认证
本插件**不需要任何 API 密钥或认证配置**，因为：
- V2EX API 是完全公开的
- 不需要注册账号或申请密钥
- 直接通过 HTTP GET 请求访问

## 连接要求和配置详情

### 网络要求
- 需要能够访问 `https://www.v2ex.com` 域名
- 支持 HTTPS 连接
- 建议稳定的网络连接以确保 API 响应

### 配置参数
插件内置以下配置，无需用户修改：
- **超时时间**: 10秒
- **用户代理**: "Dify V2EX Plugin/1.0"
- **请求头**: 自动设置 Accept: application/json

### 错误处理
插件包含完善的错误处理机制：
- 网络超时自动重试提示
- API 频率限制检测和警告
- 无效参数验证和提示
- 数据格式错误处理

## 项目结构

```
v2ex/
├── main.py                 # 插件入口文件
├── manifest.yaml          # 插件清单文件
├── requirements.txt       # Python 依赖
├── provider/
│   ├── v2ex.py           # 工具提供者实现
│   └── v2ex.yaml         # 工具提供者配置
├── tools/
│   ├── v2ex.py           # 主要工具实现
│   ├── v2ex.yaml         # 工具配置
│   └── v2ex_search.yaml  # 搜索工具配置
├── _assets/
│   ├── icon.svg          # 插件图标
│   └── icon-dark.svg     # 深色主题图标
├── README.md             # 本文档
├── GUIDE.md             # 开发指南
├── PRIVACY.md           # 隐私政策
└── api.md               # V2EX API 文档
```

## 插件源代码仓库

🔗 **GitHub 仓库**: [https://github.com/frederick/v2ex-dify-plugin](https://github.com/frederick/v2ex-dify-plugin)

在这个仓库中，您可以：
- 查看完整的源代码
- 报告问题和错误
- 提交功能请求
- 贡献代码改进
- 下载最新版本

## 开发和贡献

### 本地开发
1. 克隆仓库：`git clone https://github.com/frederick/v2ex-dify-plugin.git`
2. 安装依赖：`pip install -r requirements.txt`
3. 配置调试环境（参见上面的设置说明）
4. 运行：`python -m main`

### 提交问题
如果您遇到任何问题或有功能建议，请在 GitHub 仓库中创建 Issue。

### 贡献代码
欢迎提交 Pull Request！请确保：
- 代码符合项目风格
- 包含适当的测试
- 更新相关文档

## 许可证

本项目采用开源许可证，详情请查看 [LICENSE](LICENSE) 文件。

## 支持

如需帮助，请：
1. 查看本 README 文档
2. 阅读 [GUIDE.md](GUIDE.md) 开发指南
3. 在 GitHub 仓库提交 Issue
4. 联系作者：2313072@mail.nankai.edu.cn

---

*该插件遵循 V2EX API 使用规则，仅用于学术研究和合法用途。*

