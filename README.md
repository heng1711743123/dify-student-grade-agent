# Dify Student Grade Query Agent / Dify 学生成绩查询 Agent

[English](#english) | [中文](#中文)

---

## English

A hands-on tutorial for building a **NLP2SQL (Text2SQL) ChatFlow** on [Dify](https://dify.ai/) that connects to **MySQL**, generates SQL from natural language, and renders results as **ECharts** bar charts, line charts, and pie charts.

**Repository:** [heng1711743123/dify-student-grade-agent](https://github.com/heng1711743123/dify-student-grade-agent)

### Demo

| Bar chart — class average scores | Pie chart — grade distribution |
|:---:|:---:|
| ![Bar chart demo](docs/demo/demo-bar-chart-class-average.png) | ![Pie chart demo](docs/demo/demo-pie-chart-grade-ratio.png) |

**Example queries:**
- `查询全校各个班级的平均分情况` — Query average scores by class
- `查询高一三班学生成绩占比` — Query grade distribution for Class 高一(3)

### Features

- Natural language → SQL via LLM
- MySQL integration through `hjlarry/database` plugin
- Loop execution for multiple SQL statements
- Auto chart type selection (bar / line / pie) via ECharts tool
- Sample dataset: 110 student grade records

### Project Structure

```
├── README.md
├── docs/demo/                          # Live demo screenshots
└── 02-学生成绩查询Agent/
    ├── 01-Mysql数据库操作.md              # MySQL setup guide
    ├── 02-学生成绩查询ChatFlow.md         # Dify ChatFlow tutorial (with screenshots)
    ├── init_student_grades.sql         # Database init script
    └── img/                            # Tutorial step screenshots
```

### Quick Start

#### 1. Prepare MySQL

```bash
mysql -u root -p --default-character-set=utf8mb4
```

```sql
CREATE DATABASE dify_test;
USE dify_test;
SOURCE init_student_grades.sql;
```

> **Windows tip:** Do not pipe SQL files through PowerShell — use `mysql ... < file.sql` in CMD, or run `SOURCE` inside the MySQL client with UTF-8 charset to avoid garbled Chinese text.

#### 2. Install Dify & plugins

Install these tools in Dify before building the workflow:

- **Time** tool
- **ECharts** chart generator
- **hjlarry/database** plugin

#### 3. Configure Database URI

When Dify runs in **Docker on Windows**, use one of these hosts (replace `your_password`):

```properties
mysql+pymysql://root:your_password@host.docker.internal:3306/dify_test
mysql+pymysql://root:your_password@192.168.65.254:3306/dify_test
```

| Host | When to use |
|------|-------------|
| `host.docker.internal` | Docker Desktop (try first) |
| `192.168.65.254` | Docker Desktop gateway IP (fallback) |
| `127.0.0.1` | Dify installed locally, **not** in Docker |

> Avoid `127.0.0.1` when Dify/plugins run inside containers — it points to the container itself, not your host MySQL.

#### 4. Build the ChatFlow

Follow the step-by-step guide with screenshots:

📄 [`02-学生成绩查询Agent/02-学生成绩查询ChatFlow.md`](02-学生成绩查询Agent/02-学生成绩查询ChatFlow.md)

### Requirements

- MySQL 8.x
- Dify (Docker or local install)
- LLM API key configured in Dify
- Plugins: `hjlarry/database`, ECharts, Time

---

## 中文

基于 [Dify](https://dify.ai/) 的 **NLP2SQL（Text2SQL）ChatFlow** 实战教程：连接 **MySQL** 数据库，将自然语言转为 SQL 查询，并通过 **ECharts** 自动生成柱状图、折线图、饼图。

**仓库地址：** [heng1711743123/dify-student-grade-agent](https://github.com/heng1711743123/dify-student-grade-agent)

### 效果演示

| 柱状图 — 各班平均分 | 饼图 — 成绩占比 |
|:---:|:---:|
| ![柱状图演示](docs/demo/demo-bar-chart-class-average.png) | ![饼图演示](docs/demo/demo-pie-chart-grade-ratio.png) |

**示例问题：**
- `查询全校各个班级的平均分情况`
- `查询高一三班学生成绩占比`

### 功能特点

- 大模型将自然语言转为 SQL
- 通过 `hjlarry/database` 插件连接 MySQL
- 循环节点支持多条 SQL 批量执行
- 条件分支自动选择柱状图 / 折线图 / 饼图
- 内置 110 条学生成绩样例数据

### 目录结构

```
├── README.md
├── docs/demo/                          # 实际运行效果截图
└── 02-学生成绩查询Agent/
    ├── 01-Mysql数据库操作.md              # MySQL 建库建表教程
    ├── 02-学生成绩查询ChatFlow.md         # Dify 工作流搭建教程（含截图）
    ├── init_student_grades.sql         # 数据库初始化脚本
    └── img/                            # 教程步骤截图
```

### 快速开始

#### 1. 准备 MySQL 数据库

```bash
mysql -u root -p --default-character-set=utf8mb4
```

```sql
CREATE DATABASE dify_test;
USE dify_test;
SOURCE init_student_grades.sql;
```

> **Windows 提示：** 不要用 PowerShell 管道导入 SQL，否则中文可能变成 `??`。请用 CMD 重定向，或在 MySQL 客户端内 `SOURCE`，并指定 `utf8mb4` 字符集。

#### 2. 安装 Dify 与插件

搭建工作流前，先在 Dify 中安装以下工具：

- **时间** 工具
- **ECharts** 图表生成
- **hjlarry/database** 数据库插件

#### 3. 配置 Database URI

**Windows + Docker 版 Dify** 推荐使用以下地址（将 `your_password` 替换为你的 MySQL 密码）：

```properties
mysql+pymysql://root:your_password@host.docker.internal:3306/dify_test
mysql+pymysql://root:your_password@192.168.65.254:3306/dify_test
```

| 地址 | 适用场景 |
|------|----------|
| `host.docker.internal` | Docker Desktop（优先尝试） |
| `192.168.65.254` | Docker Desktop 网关 IP（备选） |
| `127.0.0.1` | Dify 本地源码安装（非 Docker） |

> 插件在容器内运行时，`127.0.0.1` 指向容器自身而非宿主机 MySQL，通常会连接失败。

#### 4. 搭建 ChatFlow 工作流

按教程逐步配置各节点（含完整截图）：

📄 [`02-学生成绩查询Agent/02-学生成绩查询ChatFlow.md`](02-学生成绩查询Agent/02-学生成绩查询ChatFlow.md)

### 环境要求

- MySQL 8.x
- Dify（Docker 或本地安装）
- Dify 中已配置 LLM API Key
- 插件：`hjlarry/database`、ECharts、时间工具
