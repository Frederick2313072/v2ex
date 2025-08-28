# V2EX Forum Search Plugin

[**English**](README.en.md) | [中文](README.md)

**Author:** frederick  
**Version:** 0.0.1  
**Type:** Dify tool plugin

## Plugin Description

The V2EX Forum Search Plugin is a tool plugin designed for the Dify platform. It helps users search and retrieve various content from the V2EX forum, including hot topics, latest topics, node information, and user profiles. It serves content via V2EX's public API and requires no authentication.

## Main Features

- 🔥 Fetch V2EX hot topics
- 🆕 Fetch V2EX latest topics
- 📋 Query node details
- 👤 Query user profiles
- 🔍 Support keyword filtering

## Setup Guide

### 1. Requirements

- Python 3.12+
- Dify platform
- Network access to V2EX API

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Local Debug Configuration

1. Copy the environment file:
   ```bash
   cp .env.example .env
   ```

2. Edit `.env` with the following variables:
   ```
   INSTALL_METHOD=remote
   REMOTE_INSTALL_URL=debug.dify.ai:5003  # or your Dify instance
   REMOTE_INSTALL_KEY=your_debug_key_here  # obtain from Dify plugin manager
   ```

### 4. Start the Plugin for Debugging

```bash
python -m main
```

### 5. Install the Plugin in Dify

1. Upload the `v2ex.difypkg` file in the Dify plugin manager
2. Or connect to the locally running plugin in debug mode

## Usage

### Basics

The plugin provides a tool named "V2EX content search" with the parameters below:

#### 1. search_type (required)
- **hot_topics**: Get current trending topics
- **latest_topics**: Get the latest published topics
- **node_info**: Get details of a specific node
- **user_info**: Get a user's profile

#### 2. search_query (optional)
- For hot/latest topics: optional keywords to filter content
- For node info: node name (e.g., python, javascript, apple)
- For user info: username or user ID

#### 3. limit (optional)
- Maximum number of results to return
- Default: 10
- Range: 1-50

### Examples

#### Get hot topics
```
search_type: hot_topics
search_query: (empty for all, or a keyword like "python")
limit: 10
```

#### Query node info
```
search_type: node_info
search_query: python
limit: (not applicable)
```

#### Query user info
```
search_type: user_info
search_query: Livid
limit: (not applicable)
```

### Returned Data

Structured JSON including:
- Topic: title, content, link, replies, author, node info
- Node: name, description, topic count, link
- User: username, tagline, bio, social links

## API and Authentication

### V2EX API
- **Base URL**: `https://www.v2ex.com/api`
- **Auth**: Not required; API is public
- **Rate limit**: 120 requests/hour per IP
- **Cache**: CDN-backed; repeated requests may be cached

### No Credentials Needed
This plugin requires no API key because:
- V2EX API is fully public
- No account or key application is needed
- Access via HTTP GET directly

## Connectivity and Configuration

### Network
- Must be able to access `https://www.v2ex.com`
- HTTPS supported
- Stable connection recommended

### Built-in Config
The plugin ships with sane defaults:
- **Timeout**: 10s
- **User-Agent**: "Dify V2EX Plugin/1.0"
- **Headers**: Accept: application/json

### Error Handling
Includes robust handling:
- Timeout hints and retries
- Rate-limit detection and warnings
- Parameter validation
- Malformed data handling

## Project Structure

```
v2ex/
├── main.py                 # Entry
├── manifest.yaml           # Manifest
├── requirements.txt        # Python deps
├── provider/
│   ├── v2ex.py             # Provider implementation
│   └── v2ex.yaml           # Provider config
├── tools/
│   ├── v2ex.py             # Core tool implementation
│   ├── v2ex.yaml           # Tool config
│   └── v2ex_search.yaml    # Search tool config
├── _assets/
│   └── icon.svg            # Plugin icon
├── README.md               # Chinese README
├── README.en.md            # English README
├── GUIDE.md                # Guide
├── PRIVACY.md              # Privacy
├── api.md                  # V2EX API doc
└── v2ex.difypkg            # Package file
```

## Repository

🔗 **GitHub**: [https://github.com/frederick/v2ex-dify-plugin](https://github.com/frederick/v2ex-dify-plugin)

You can:
- Browse source code
- Report issues
- Request features
- Contribute improvements
- Download releases

## Development and Contribution

### Local Development
1. Clone: `git clone https://github.com/frederick/v2ex-dify-plugin.git`
2. Install: `pip install -r requirements.txt`
3. Configure debug (see Setup Guide)
4. Run: `python -m main`

### Issues
Open an issue on GitHub for bugs or requests.

### Pull Requests
Contributions are welcome. Please ensure:
- Code style consistency
- Adequate tests
- Updated docs

## License

This project is open source. See [LICENSE](LICENSE).

## Support

If you need help:
1. Read this README
2. Check [GUIDE.md](GUIDE.md)
3. Open a GitHub issue
4. Contact the author: 2313072@mail.nankai.edu.cn

---

This plugin complies with V2EX API usage rules and is for academic and lawful use only.


