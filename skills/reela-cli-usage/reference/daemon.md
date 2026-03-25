# Daemon Internals

The `reela daemon` runs a background process that subscribes to task events and automatically delivers completed videos.

## Architecture

1. **SQS Provisioning:** On start, calls `POST /api/sqs/provision` to get a per-user SQS queue URL + STS temporary credentials
2. **Credential Refresh:** Caches STS credentials, auto-refreshes when within 5 minutes of expiry
3. **Long-Polling Loop:** Polls SQS with 20-second wait, receives up to 10 messages per batch
4. **Event Dispatch:** Routes messages to handler registry by task status

## Delivery Flow (on task completion)

When a task reaches status `130` (completed):

1. Fetches presigned download URL from `GET /api/tasks/{task_id}/download`
2. Streams download to temp file (`.{task_id}.mp4.tmp`)
3. Atomic rename to `{task_id}.mp4` in the download directory
4. Sends OS notification: "Reela: Video completed" (prompt truncated to 50 chars)

When a task reaches status `10` (failed):

1. Sends OS notification: "Reela: Video rendering failed"

## Configuration

| Key | Default | Description |
|-----|---------|-------------|
| `delivery.download` | `~/Videos/reela` | Download directory (tilde-expanded) |
| `delivery.notify` | `true` | Enable/disable OS notifications |

## System Service Installation

**macOS:** LaunchAgent plist at `~/Library/LaunchAgents/com.reela.daemon.plist` (RunAtLoad, KeepAlive)

**Linux:** systemd user unit at `~/.config/systemd/user/reela-daemon.service` (Restart=on-failure, RestartSec=10)

## Process Management

- PID file: `~/.reela/daemon.pid`
- Log file: `~/.reela/daemon.log` (verbosity via `RUST_LOG` env var)
- Background mode: re-execs with `--foreground`, detaches via `setsid()`
- Stop: sends SIGTERM, waits 10s, then SIGKILL
- Graceful shutdown on SIGTERM and Ctrl+C
