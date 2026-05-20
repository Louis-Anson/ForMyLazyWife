
## 🗓️ 需求列表


<div align="center">

[![Project Status](https://img.shields.io/badge/Status-规划中-orange?style=flat-square)]()
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Ready-18BCF2?logo=homeassistant&logoColor=white&style=flat-square)]()
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?logo=docker&logoColor=white&style=flat-square)]()

</div>


| 需求层级 | 模块/子系统 | 功能描述 | 状态 | 优先级 | 推荐工具/方案 | 部署位置 | 关键配置/备注 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 统一交互入口 | 微信机器人对话入口 | 自然语言指令下达与结果反馈 | 未开发 | 高 | OpenClaw + 微信ClawBot插件 / 企业微信 | NAS Docker | 日常对话用 ClawBot；系统通知用企业微信主动推送 |
| 统一交互入口 | 微信小程序前端 | 图形化查看数据、图表、手动录入 | 未开发 | 高 | uni-app 开发 + API 网关 | NAS + 微信小程序后台 | 通过 Traefik 网关统一对外暴露，强制 HTTPS |
| AI调度中枢层 | 意图识别与任务分发 | 解析自然语言并路由到对应子系统 | 未开发 | 高 | OpenClaw Gateway + 大模型（由 New-API 统一管理） | NAS Docker | OpenClaw 技能指向 New-API 地址，由 New-API 负载均衡和成本控制 |
| AI调度中枢层 | AI 模型接口管理 | 统一管理多个大模型 API，提供标准化接口、额度控制和负载均衡 | 未开发 | 高 | New-API | NAS Docker | 对接 DeepSeek、通义千问等；支持多用户隔离和 Token 预算 |
| AI调度中枢层 | 统一通知推送 | 将各子系统事件推送到微信 | 未开发 | 高 | ntfy + OpenClaw → 企业微信主动通知 | NAS Docker | 日常提醒由 ClawBot 被动回复；系统级通知走企业微信 |
| API 网关与统一入口 | 反向代理与 SSL 终结 | 统一对外入口，自动签发和续期 SSL 证书，路由请求到内部服务 | 未开发 | 高 | Traefik | NAS Docker | 监听 80/443 端口，通过 Docker Labels 自动发现服务；替代 NPM |
| API 网关与统一入口 | 网关可视化管理 | 提供 Web UI 管理 Traefik 路由、证书和中间件 | 未开发 | 中 | Traefik Manager | NAS Docker | 内网访问，简化后期运维 |
| 家庭任务系统 | 任务编排与状态跟踪 | 一句话创建任务、查看进度、评论互动 | 未开发 | 高 | Donetick | NAS Docker | 通过 Traefik 路由，内网服务不暴露公网端口 |
| 家庭任务系统 | 菜谱录入与点餐 | 菜谱管理、膳食计划、根据食材推荐 | 未开发 | 高 | Tandoor Recipes | NAS Docker | 与 Grocy 库存联动；内网服务 |
| 食物状态系统 | 库存管理 | 品类、数量、采购日期、保质期管理 | 未开发 | 高 | Grocy | NAS Docker | 支持条码扫描；自定义临期提醒；内网服务 |
| 食物状态系统 | 烹饪建议 | 根据现有食材推荐可制作菜肴 | 未开发 | 高 | OpenClaw 调用 Grocy + Tandoor API | NAS Docker | 通过 API 网关转发，内网服务 |
| 家庭资产管理 | 衣物/鞋帽/床上用品管理 | 记录购买时间、使用状态、清洗周期，支持特殊衣物（冲锋衣/滑雪服）维护提醒 | 未开发 | 高 | Homebox | NAS Docker | 通过 API 与 AI 调度中枢集成，支持多用户；镜像：sysadminsmedia/homebox |
| 家用记账系统 | 收支记录与统计 | 收入/支出分类记录、图表分析、实时查询 | 未开发 | 高 | ezBookkeeping | NAS Docker | 内网服务；支持微信/支付宝账单导入 |
| 家用记账系统 | 微信触发记账 | 通过微信消息自动添加记账条目 | 未开发 | 高 | OpenClaw + ezBookkeeping API | NAS Docker | 通过 API 网关转发 |
| 智能家居中枢 | 设备统一接入与控制 | 接入空调、洗衣机、门锁、传感器等 | 未开发 | 高 | Home Assistant OS (虚拟机) | QNAP Virtualization Station | 桥接网络，独立 IP；通过 Traefik 代理并信任转发 |
| 多媒体系统 | 小说下载与搜刮 | 聚合多平台搜索下载小说，支持 TXT/EPUB 导出，提供 Web 界面 | 未开发 | 中 | Go Novel DL | NAS Docker | 与音乐服务共享 traefik 网络，通过域名访问；支持定时追更 |
| 多媒体系统 | 音乐下载与搜刮 | 聚合 10+ 平台搜索下载无损音乐，支持歌单导入与加密解密 | 未开发 | 中 | Go Music DL | NAS Docker | 提供 Web 界面，与 Navidrome 共享音乐目录 |
| 多媒体系统 | 私人音乐服务器 | 搭建私人曲库，多设备在线播放，支持 AirPlay 投送 HomePod | 未开发 | 中 | Navidrome | NAS Docker | 兼容 Subsonic API，通过 OpenClaw 技能触发播放 |
| 多媒体系统 | 照片备份与管理 | 自动备份手机照片，支持人脸识别与多用户 | 未开发 | 高 | Immich | NAS Docker | 替代 Google Photos，数据完全本地化 |
| 智能家居控制 | 格力空调控制 | 开关、调温、模式切换 | 未开发 | 低 | HA + Gree 集成 | 集成于 HA | 局域网本地控制 |
| 智能家居控制 | 美的洗衣机/烘干机控制 | 启动/暂停、模式选择 | 未开发 | 低 | HA + Midea AC LAN 集成 | 集成于 HA | 可能需降级固件 |
| 安防监控接入 | 可视门铃/监控本地存储 | 视频流 24 小时录制到 NAS | 未开发 | 低 | Reolink / Aqara G410 (支持 RTSP) | 自家 | 通过 Frigate 进行 AI 分析 |
| 安防监控接入 | AI 人脸识别与联动 | 区分家人/陌生人并触发自动化 | 未开发 | 低 | Frigate + HA | NAS Docker (需 SSD) | 本地 AI 处理；可联动通知 |
| 健康监测集成 | 经期记录与预测 | 自动同步 Apple Watch 数据并 AI 预测周期 | 未开发 | 高 | Health Auto Export + HA + 自建 LSTM 模型 | NAS + iPhone | 数据本地处理；隐私优先 |
| 健康监测集成 | 经期提醒与养生茶饮任务 | 经期前 3 天提醒；定期推送养生茶饮提醒 | 未开发 | 高 | HA 自动化 → Donetick 创建任务 → OpenClaw 推送微信 | NAS Docker | 任务闭环管理 |
| 数据存储层 | 统一数据库 | 存储各子系统结构化数据及 AI 模型数据 | 未开发 | 高 | PostgreSQL (主) + SQLite (子系统内置) | NAS Docker (SSD 加速) | 使用 PgBouncer 连接池 |
| 网络与安全 | 统一入口与 HTTPS | 为所有服务提供安全的对外访问 | 未开发 | 高 | Traefik 自动 Let's Encrypt | NAS Docker | 仅开放 80/443；内部服务完全隐藏 |
| 硬件平台 | NAS 设备 | QNAP TS-464C2: N5095/8GB RAM/4TB HDD + 128GB SSD | 已完成 | 高 | QNAP Container Station + Virtualization Station | 本地 | SSD 用于 Docker 热数据；HDD 用于存储 |
| 扩展性设计 | 新需求接入方式 | 任意带 API 的服务均可无缝加入 | 未开发 | 高 | 在 OpenClaw 中添加技能；在 Traefik 中添加路由标签 | NAS Docker | 遵循“部署服务 → 配置标签 → 定义技能”标准流程 |
