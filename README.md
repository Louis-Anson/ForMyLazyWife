# Ai Jia S

🏠 一个跑在 NAS 上的家庭AI管家：微信一句话指挥家务、管理冰箱库存、自动记账，还偷偷记住了她的生理期。全本地部署，数据主权归家。

# 🏠 AiJiaS / 家务OS

> *"用代码写一封给家的情书。S for Sweet，S for Her."*
> *"代码是冷的，但日子是热的。用一台 NAS，给老婆搭个隐形的家庭管家。"*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Ready-blue)](https://www.home-assistant.io/)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?logo=docker&logoColor=white)](https://www.docker.com/)
[![Privacy First](https://img.shields.io/badge/Privacy-Local%20Only-green)]()


## 📖 项目起源

老婆有一天刷手机，说想要一个能听懂人话的管家，对着微信说句话就能安排家务、管冰箱、记账单。  
我整理完她的需求后，发现这不止是做个机器人，而是要把整个家“数字化”一遍。  
于是，这个项目诞生了

## 🎯 它能做什么？

- 💬 **微信一句话指挥**：通过 OpenClaw 机器人，在微信里用自然语言安排任务、查询库存、记账。
- 📱 **小程序可视化**：家人用微信小程序查看冰箱存货、家庭账本、任务进度。
- 🗓️ **家庭任务系统**：基于 Donetick，自动编排家务，完成情况实时通知。
- 🥦 **食物状态管理**：基于 Grocy，记录食材采购/过期时间，临期自动提醒，还能根据库存推荐菜谱。
- 💰 **家用记账**：基于 ezBookkeeping，支持手动/微信触发记账，分类统计一目了然。
- 👕 **家庭资产管理**：基于 Homebox，管理衣物、鞋帽、床上用品等生活物品的购买时间、使用状态和清洗维护周期。
- 🎵 **媒体服务**：Immich 管理全家照片，Navidrome 搭建私人音乐库。
- 🌡️ **智能家居中枢**：Home Assistant 统一接入格力空调、美的洗衣机等设备。
- ❤️ **健康关怀（隐藏功能）**：接入 Apple Watch 数据，AI 预测生理期，提前提醒煮五红汤、苹果黄芪水。

## 🧱 技术架构

- **网关**：Traefik 统一入口，自动 SSL，内外分离
- **AI 调度**：OpenClaw + New-API（大模型统一管理）
- **数据库**：PostgreSQL + PgBouncer 连接池
- **智能家居**：Home Assistant OS（虚拟机）
- **部署方式**：Docker Compose + QNAP Virtualization Station
- **隐私优先**：100% 本地部署，敏感数据不出门

## 📁 仓库目录结构
```tree
AiJiaS/
├── README.md # 项目总览（本文件）
├── LICENSE # 开源协议
├── .gitignore
│
├── docs/ # 📚 文档中心
│ ├── architecture.md # 系统架构图（Mermaid）
│ ├── requirements.md # 需求跟踪表
│ ├── hybrid-deployment.md # HAOS虚拟机 + Docker混合部署总览
│ ├── haos-npm-setup.md # HAOS 接入 Traefik 指南
│ ├── agent-trial-plan.md # AI Agent 并行试用评估计划
│ ├── homebox-setup.md # Homebox 部署与集成指南
│ └── changelog.md # 变更日志
│
├── docker-compose/ # 🐳 服务编排
│ ├── core-services.yml # OpenClaw, Hermes Agent, ntfy, PostgreSQL, New-API
│ ├── traefik.yml # Traefik + Traefik Manager
│ ├── family-systems.yml # Donetick, Grocy, Tandoor, ezBookkeeping, TREK, Homebox
│ ├── media.yml # Immich, Navidrome, Go Music DL, Go Novel DL
│ ├── ai-models.yml # period-predictor
│ ├── chat.yml # silly-tavern
│ └── .env.example # 环境变量模板
│
├── openclaw/ # 🧠 AI 调度中枢（OpenClaw）
│ ├── gateway-config.yaml
│ └── skills/
│  ├── home-assistant.yaml
│  ├── family-tasks.yaml
│  ├── food-management.yaml
│  ├── bookkeeping.yaml
│  ├── health-query.yaml
│  ├── travel-planner.yaml
│  ├── music-control.yaml
│  ├── homebox.yaml
│  └── laundry-reminder.yaml
│
├── hermes/ # 🧠 AI 调度中枢（Hermes Agent，评估中）
│ └── skills/ # Hermes 技能配置目录
│  └── README.md # 技能开发说明
│
├── home-assistant/ # 🏡 智能家居配置
│ ├── configuration.yaml
│ ├── automations.yaml
│ ├── sensors.yaml
│ ├── input_datetime.yaml
│ └── customize.yaml
│
├── ai-models/ # 🤖 AI 模型
│ └── period-predictor/
│  ├── training/
│  ├── inference/
│  └── README.md
│
├── scripts/ # 🔧 运维脚本
│ ├── backup-db.sh
│ ├── health-check.sh
│ └── sync-ha-config.sh
│
├── miniprogram/ # 📱 微信小程序（预留）
│ └── README.md
│
└── assets/ # 🖼️ 静态资源
 └── architecture.png

```

## 🚀 快速开始
```bash
git clone https://github.com/你的用户名/AiJiaS.git
cd AiJiaS
...

