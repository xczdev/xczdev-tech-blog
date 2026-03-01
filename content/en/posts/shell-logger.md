---
title: "Creat a logger in Shell script"
date: 2026-03-02
tags: ["Linux", "Security"]
language: "en"
weight: 1
---

```shell
#!/bin/bash

# Set desired log level (1=WARN, 2=INFO, 3=DEBUG)
LOG_LEVEL=${LOG_LEVEL:-2}

log() {
    local level_name=$1
    local level_value=$2
    shift 2
    if [ "$LOG_LEVEL" -ge "$level_value" ]; then
        # Use stderr for logs to keep stdout clean for data
        printf "[%-5s] %s\n" "$level_name" "$*" >&2
    fi
}

# Helper aliases
warn()  { log "WARN"  1 "$@"; }
info()  { log "INFO"  2 "$@"; }
debug() { log "DEBUG" 3 "$@"; }

# --- Usage Examples ---
info "Starting the process..."
debug "Connecting to database at 127.0.0.1"

if [ ! -f "config.cfg" ]; then
    warn "Config file missing, using defaults."
fi
```