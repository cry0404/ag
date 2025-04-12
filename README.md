# OpenRouter Simple AG - Your Command-Line AI Assistant
这只是一个用 ai 编写的小玩具，稍微由我检查并且修改了其中的一小部分，难免会存在问题😂

`ag` (AI Generalist) is a simple command-line tool written in Fish shell script that allows you to interact with AI models via the OpenRouter API directly from your terminal. It supports streaming responses and managing multiple conversation contexts.

Inspired by the need for a straightforward, terminal-based AI interaction tool without heavy dependencies.

---

**[中文说明 (Chinese Description Below)](https://github.com/cry0404/Openrouter-simple-ag/blob/main/README.md#%E4%B8%AD%E6%96%87%E8%AF%B4%E6%98%8E)**

---

## Features

*   **Direct API Interaction**: Communicates with the OpenRouter API (`/chat/completions` endpoint).
*   **Streaming Responses**: Displays AI responses word-by-word as they arrive (plain text only).
*   **Named Context Management**:
    *   Maintain multiple independent conversation histories using simple named files (`-s <name>`).
    *   List available contexts (`-l`).
    *   Delete specific contexts (`-d <name>`).
    *   Default mode is ephemeral (no context loaded or saved).
*   **Customizable**: Easily change the default AI model or API endpoint within the script.
*   **Lightweight**: Primarily relies on `fish`, `curl`, and `jq`.
*   **Easy Setup & Removal**: Includes a setup script for Debian/Ubuntu-based systems with language selection and an uninstall option.

## Installation (Debian/Ubuntu based systems)

An automated setup script is provided to install dependencies and the `ag` function itself.

1.  **Download the Setup Script:**
    ```bash
    # Download directly from this repository
    curl -o setup_ag_tool.sh https://raw.githubusercontent.com/cry0404/Openrouter-simple-ag/main/setup_ag_tool.sh
    # --- OR ---
    # Clone the repository and navigate into it
    # git clone https://github.com/cry0404/Openrouter-simple-ag.git
    # cd Openrouter-simple-ag
    ```

2.  **Make it Executable:**
    ```bash
    chmod +x setup_ag_tool.sh
    ```

3.  **Run the Script:** The script will first ask you to choose a language (English/Chinese) for instructions.
    ```bash
    ./setup_ag_tool.sh
    ```
    The script will install dependencies (`fish`, `jq`, `curl`) using `apt`. It will place the `ag.fish` script in `~/.config/fish/functions/`.
    *   **Note:** Requires Fish Shell version 3.0 or higher.

4.  **Set API Key:** This is crucial! Set your OpenRouter API key as an environment variable. Run this in your terminal and add it to your `~/.config/fish/config.fish` file for persistence:
    ```fish
    set -gx OPENROUTER_API_KEY 'sk-or-v1-YOUR-API-KEY-HERE'
    # (Replace with your actual key)
    ```

5.  **Start a NEW Fish Shell:** Open a new terminal window or type `fish` to start a new session. This ensures the function is loaded.

## Uninstallation

To remove the `ag` tool:

1.  Run the setup script with the `--uninstall` flag:
    ```bash
    ./setup_ag_tool.sh --uninstall
    ```
2.  The script will remove the `ag.fish` function file.
3.  It will then **prompt you** to confirm if you want to remove the context data directory (`~/.local/share/ag_contexts`), which contains all your saved chat histories.
4.  System packages (`fish`, `jq`, `curl`) are **not** automatically removed. You can remove them manually if no longer needed (e.g., `sudo apt remove fish jq curl`).

## Usage

The basic syntax is: `ag [OPTIONS] "YOUR PROMPT"`

**Examples:**

*   Simple query (streaming plain text):
    ```bash
    ag "What is the capital of France?"
    ```

*   Start or continue a named conversation context:
    ```bash
    ag -s learning_fish "What are functions in Fish shell?"
    ag -s learning_fish "How do I define arguments for them?"
    ```

*   List saved contexts:
    ```bash
    ag -l
    ```

*   Delete a context:
    ```bash
    ag -d learning_fish
    ```

*   View help:
    ```bash
    ag -h
    ```

## Configuration

*   **API Key**: Set the `OPENROUTER_API_KEY` environment variable (mandatory).
*   **Model**: Edit the `ag.fish` file (`~/.config/fish/functions/ag.fish`) directly to change the `model_name` variable if desired.
*   **Context Directory**: Context files are stored in `~/.local/share/ag_contexts/`.

## Dependencies

*   **Required**:
    *   `fish` (Shell) Version 3.0 or higher is required.
    *   `jq`
    *   `curl`

## Troubleshooting

*   **Command 'ag' not found or `source: Error while reading file...`**:
    *   Ensure you have started a **new** Fish shell session after running the setup script.
    *   Verify your Fish version: Run `fish --version`. This script requires Fish 3.0 or higher. If your version is older (e.g., 2.x), you need to upgrade Fish shell itself via your system's package manager (e.g., `sudo apt update && sudo apt install fish`).
    *   Check if `~/.config/fish/functions/ag.fish` exists and has the correct content. You might need to re-run the setup script.
*   **Context not saving/loading**: Ensure the context directory (`~/.local/share/ag_contexts/`) and its parent directories are writable by your user. Check the contents of the `.json` files within that directory to see if they are valid JSON arrays.

## Contributing

This is just a small toy generated by AI, there are bound to be many loopholes, feel free to try modifying it to make it more convenient! 

---

# 中文说明

`ag` (AI Generalist) 是一个用 Fish shell 脚本编写的简单命令行工具，允许您直接从终端通过 OpenRouter API 与 AI 模型进行交互。它支持流式响应和管理多个对话上下文。

灵感来源于对一个直接、基于终端、无过多重依赖的 AI 交互工具的需求。

---

## 功能特性

*   **直接 API 交互**: 与 OpenRouter API 的 `/chat/completions` 端点通信。
*   **流式响应**: 逐字显示 AI 的响应（纯文本）。
*   **命名上下文管理**:
    *   使用简单的命名文件 (`-s <名称>`) 维护多个独立的对话历史。
    *   列出可用的上下文 (`-l`)。
    *   删除指定的上下文 (`-d <名称>`)。
    *   默认模式为即时对话（不加载也不保存上下文）。
*   **可定制**: 可在脚本中轻松更改默认 AI 模型或 API 端点。
*   **轻量级**: 主要依赖 `fish`, `curl`, `jq`。
*   **易于设置与移除**: 为基于 Debian/Ubuntu 的系统提供了一键安装脚本（带语言选择）和卸载选项。

## 安装 (基于 Debian/Ubuntu 的系统)

提供了一个自动化安装脚本来安装依赖项和 `ag` 函数本身。

1.  **下载安装脚本:**
    ```bash
    # 直接从本仓库下载
    curl -o setup_ag_tool.sh https://raw.githubusercontent.com/cry0404/Openrouter-simple-ag/main/setup_ag_tool.sh
    # --- 或者 ---
    # 克隆仓库并进入目录
    # git clone https://github.com/cry0404/Openrouter-simple-ag.git
    # cd Openrouter-simple-ag
    ```

2.  **使其可执行:**
    ```bash
    chmod +x setup_ag_tool.sh
    ```

3.  **运行脚本:** 脚本会首先提示您选择安装语言 (英文/中文)。
    ```bash
    ./setup_ag_tool.sh
    ```
    脚本将使用 `apt` 安装依赖项 (`fish`, `jq`, `curl`)。它会将 `ag.fish` 脚本放置在 `~/.config/fish/functions/`。
    *   **注意：**需要 Fish Shell 3.0 或更高版本。

4.  **设置 API 密钥:** 非常重要！将您的 OpenRouter API 密钥设置为环境变量。在终端中运行此命令，并将其添加到您的 `~/.config/fish/config.fish` 文件中以持久化：
    ```fish
    set -gx OPENROUTER_API_KEY 'sk-or-v1-你的API密钥放在这里'
    # (替换为您的真实密钥)
    ```

5.  **启动一个新的 Fish Shell:** 打开一个新的终端窗口或输入 `fish` 来启动新会话。这确保函数被加载。

## 卸载

要移除 `ag` 工具：

1.  使用 `--uninstall` 标志运行安装脚本：
    ```bash
    ./setup_ag_tool.sh --uninstall
    ```
2.  脚本将移除 `ag.fish` 函数文件。
3.  然后它会**提示您**确认是否要移除上下文数据目录 (`~/.local/share/ag_contexts`)，该目录包含所有已保存的聊天记录。
4.  系统软件包 (`fish`, `jq`, `curl`) **不会**被自动移除。如果不再需要，您可以手动移除它们 (例如 `sudo apt remove fish jq curl`)。

## 使用方法

基本语法: `ag [选项] "你的提示"`

**示例:**

*   简单查询 (流式纯文本):
    ```bash
    ag "法国的首都是哪里？"
    ```

*   开始或继续一个命名对话上下文:
    ```bash
    ag -s 学习fish "Fish shell 中的函数是什么？"
    ag -s 学习fish "如何为它们定义参数？"
    ```

*   列出已保存的上下文:
    ```bash
    ag -l
    ```

*   删除一个上下文:
    ```bash
    ag -d 学习fish
    ```

*   查看帮助:
    ```bash
    ag -h
    ```

## 配置

*   **API 密钥**: 必须设置 `OPENROUTER_API_KEY` 环境变量。
*   **模型**: 可直接编辑 `ag.fish` 文件 (`~/.config/fish/functions/ag.fish`) 来更改 `model_name` 变量。
*   **上下文目录**: 上下文文件存储在 `~/.local/share/ag_contexts/`。

## 依赖

*   **必需**:
    *   `fish` (Shell) 需要 3.0 或更高版本。
    *   `jq`
    *   `curl`

## 问题排查

*   **Command 'ag' not found 或 `source: Error while reading file...`**:
    *   确保在运行安装脚本后已启动**新的** Fish shell 会话。
    *   验证您的 Fish 版本: 运行 `fish --version`。此脚本需要 Fish 3.0 或更高版本。如果您的版本较旧 (例如 2.x)，您需要通过系统的包管理器升级 Fish shell (例如 `sudo apt update && sudo apt install fish`)。
    *   检查 `~/.config/fish/functions/ag.fish` 是否存在且内容正确。您可能需要重新运行安装脚本。
*   **上下文未保存/加载**: 确保上下文目录 (`~/.local/share/ag_contexts/`) 及其父目录对您的用户可写。检查该目录下的 `.json` 文件内容是否为有效的 JSON 数组。

## 贡献

这只是一个由 ai 生成的小玩具，难免有许多漏洞，你可以来尝试修改使其变得更加方便！
