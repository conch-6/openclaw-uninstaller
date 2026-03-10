---
name: openclaw-uninstaller
description: Completely and thoroughly uninstall OpenClaw (AI assistant) from the current system, leaving no residual files, configs, processes, or environment variables. Use this skill whenever the user asks to uninstall, remove, clean up, or wipe OpenClaw or any AI assistant installed on the device. Triggers on phrases like "卸载 openclaw", "uninstall openclaw", "remove openclaw", "clean up AI", "彻底卸载", or any request to generate an uninstall script for OpenClaw.
---

# OpenClaw Uninstaller Skill

完全彻底地从当前系统卸载 OpenClaw，不留任何残留文件、配置、进程或环境变量。

---

## 执行流程

### 第一步：系统环境信息采集

在生成任何脚本之前，必须先全面了解当前系统环境。需要采集的信息包括：

- 操作系统类型、发行版和版本
- 当前用户身份和主目录路径
- 使用的 Shell 类型及其配置文件位置
- 系统中所有与 openclaw 相关的文件和目录（全盘搜索）
- 当前正在运行的所有 openclaw 相关进程
- 系统中已安装的包管理器（apt、yum、brew、snap、flatpak、npm、pip 等）及其中是否有 openclaw
- openclaw 的二进制文件位置
- 系统服务中是否有 openclaw 相关条目（systemd、launchd、init.d 等）
- 各 Shell 配置文件中是否存在 openclaw 相关的环境变量或 PATH 设置
- 定时任务（cron）中是否有 openclaw 相关条目
- 临时目录中是否有 openclaw 相关文件

采集完毕后，综合分析结果，然后进入第二步。

---

### 第二步：生成卸载脚本 uninstall_ai.sh

根据第一步采集到的真实信息，编写一个名为 `uninstall_ai.sh` 的卸载脚本。脚本必须做到：

脚本内容要分步骤、有条理，每一步都要有清晰的说明输出，让用户知道当前正在执行什么操作。脚本整体要足够健壮，即使某些路径不存在或某些操作失败，也不应中断整个卸载流程。

脚本需要覆盖以下所有方面，具体路径和方式完全根据第一步的实际发现来决定：

**进程清理**：终止所有正在运行的 openclaw 相关进程。

**服务清理**：停止并禁用所有 openclaw 相关的系统服务，并删除对应的服务配置文件。

**二进制文件清理**：删除所有 openclaw 可执行文件。

**配置目录清理**：删除用户目录和系统目录下所有 openclaw 相关的配置文件夹和配置文件。

**数据与日志清理**：删除 openclaw 的数据目录、日志目录和缓存目录。

**包管理器卸载**：通过检测到的包管理器正式卸载 openclaw 软件包。

**环境变量清理**：从所有 Shell 配置文件中删除 openclaw 相关的环境变量、PATH 条目和别名设置。

**定时任务清理**：从 crontab 中删除所有 openclaw 相关条目。

**临时文件清理**：清除临时目录中所有 openclaw 相关文件。

**最终验证**：卸载完成后，在全系统范围内搜索是否还存在任何 openclaw 相关的文件或进程，并将结果报告给用户。如果干净则确认卸载成功，如有残留则列出具体路径。

脚本完成后保存到当前工作目录，并赋予可执行权限。

---

### 第三步：执行脚本

执行生成好的脚本，完整捕获并展示执行输出，让用户清楚地看到每一步的执行结果，以及最终是否彻底卸载成功。

---

## 注意事项

- 第一步的系统采集是强制要求，禁止跳过直接生成通用脚本。
- 脚本内容必须基于真实发现，而不是假设或模板。
- 如果当前用户权限不足以执行某些操作，需提示用户可能需要 sudo 权限。
- 脚本中每一个删除操作都要确保即使目标不存在也不会报错退出。