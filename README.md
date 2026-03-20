# Reela CLI

Command-line interface for [Reela](https://reela.com) — create AI-powered videos from your terminal.

## Installation

### Install with AI Agent

Tell your agent:

> Follow https://github.com/reelanything/reela-cli/blob/main/INSTALL.md to install Reela CLI and skills.

### Manual Install (Linux / macOS)

```sh
curl -fsSL https://raw.githubusercontent.com/reelanything/reela-cli/main/install.sh | bash
```

### Windows

Download the `.zip` archive from the [latest release](https://github.com/reelanything/reela-cli/releases/latest), extract `reela.exe`, and add its location to your `PATH`.

### Install skills

```sh
npx skills add https://github.com/reelanything/reela-cli -g
```

## Quick Start

```sh
# Log in to your Reela account
reela login

# Create a video
reela create -p "A 30-second product demo for my app"

# Check video status
reela status

# View all tasks
reela tasks
```

## Commands

| Command  | Description                          |
| -------- | ------------------------------------ |
| `login`  | Authenticate with your Reela account |
| `logout` | Remove stored credentials            |
| `whoami` | Show current authenticated user      |
| `create` | Create a new video                   |
| `status` | Check status of recent tasks         |
| `tasks`  | List all tasks                       |
| `config` | Manage CLI configuration             |

## Configuration

Configuration is stored in `~/.config/reela/`. Use `reela config` to manage profiles and settings.

## License

Proprietary. See [reela.com](https://reela.com) for terms of service.
