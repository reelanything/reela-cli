---
name: reela-cli-usage
description: Reela CLI command reference for AI agents. Always load this skill before using any `reela` command.
version: 0.1.0
---

# Reela CLI Usage

## Install / Update

If `reela` is not installed or you need to update, follow the install guide:

> https://github.com/reelanything/reela-cli/blob/main/INSTALL.md

Quick reference for the `reela` command-line tool.

## Authentication

- `reela login` — OAuth Device Flow login (outputs JSON stages)
- `reela logout` — Remove stored credentials
- `reela whoami` — Display current user info (JSON)

## Video Creation

- `reela create <prompt> [flags]` — Create a new video task
- `reela create --prompt-file <path> [flags]` — Create from prompt file
- Key flags: `--duration`, `--layout`, `--tier`, `--visual`, `--avatar`, `--file`, `--session`, `--dry-run`, `--idempotency-key`

## Task Management

- `reela tasks list [--status <n>] [--limit <n>] [--offset <n>] [--sort <field:dir>]` — List tasks (sort default: `created_at:desc`)
- `reela tasks get <id>` — Get task details
- `reela tasks download <id> [-o <path>]` — ⚠️ Not yet implemented
- `reela tasks retry <id>` — ⚠️ Not yet implemented

## Status & Config

- `reela status` — Global status (auth, daemon, delivery, quota)
- `reela config set <key> <value>` — Set config value
- `reela config get <key>` — Get config value
- `reela config list` — List all config
- `reela config profiles list` — List all profiles
- `reela config profiles use <name>` — Set the active profile

## Daemon

The daemon is a background process that subscribes to task completion events via SQS long-polling and performs automatic delivery (download + OS notification).

**Commands:**
- `reela daemon start [--foreground]` — Start background daemon
- `reela daemon stop` — Stop daemon
- `reela daemon status` — Check daemon status (running, PID, uptime)
- `reela daemon install` — Install as system service (auto-start on boot)
- `reela daemon uninstall` — Uninstall the system service
- `reela daemon logs --tail <n>` — View recent logs

**Behavior:** When running, the daemon automatically downloads completed videos to `delivery.download` dir (default `~/Videos/reela`) and sends OS notifications. See [daemon.md](./reference/daemon.md) for details.

**Config keys:**
- `delivery.download` — Download directory (default: `~/Videos/reela`)
- `delivery.notify` — Enable OS notifications (default: `true`)

## Global Flags

`--profile <name>`, `--api-base <url>`, `--output json|table|plain`, `--no-color`, `--verbose`

## Environment Variables

`REELA_PROFILE`, `REELA_API_BASE`, `REELA_OUTPUT`, `REELA_COLLECTION_ID`, `RUST_LOG` (daemon log level)

## File System Locations

| Path | Purpose |
|------|---------|
| `~/.reela/config.toml` | CLI configuration |
| `~/.reela/credentials.json` | Stored OAuth credentials |
| `~/.reela/daemon.pid` | Daemon PID file |
| `~/.reela/daemon.log` | Daemon log file |
| `~/.config/reela/sessions.json` | Session-to-collection index |
| `~/Videos/reela/` | Default download directory |

## Exit Codes

| Code | Meaning         |
| ---- | --------------- |
| 0    | Success         |
| 1    | General error   |
| 2    | Auth failure    |
| 3    | Bad request     |
| 4    | Not found       |
| 5    | Quota exhausted |
| 6    | Timeout         |

## Task Status Codes

| Code | Label      |
| ---- | ---------- |
| 0    | cancelled  |
| 1    | pending    |
| 2    | processing |
| 10   | failed     |
| 26   | partial    |
| 130  | completed  |

## Update

To update reela-cli and this skill, fetch the install guide for instructions:

https://raw.githubusercontent.com/reelanything/reela-cli/main/INSTALL.md

## Reference

Detailed documentation is available in the `reference/` directory:

| File                                             | Description                                                                          |
| ------------------------------------------------ | ------------------------------------------------------------------------------------ |
| [create-params.md](./reference/create-params.md) | `reela create` 命令的完整参数说明，包括必选/可选参数、Visual 类型枚举和用法示例      |
| [file-attachments.md](./reference/file-attachments.md) | 文件附件指南，说明如何通过 `--file` 标志上传图片、视频、音乐作为素材 |
| [tiers.md](./reference/tiers.md)                 | 视频质量等级对比表，包含各等级的画质、速度、积分消耗及推荐场景                       |
| [daemon.md](./reference/daemon.md)                 | Daemon 内部机制：SQS 订阅、自动下载、OS 通知、系统服务安装              |
