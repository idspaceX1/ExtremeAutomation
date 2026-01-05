# ExtremeAutomation

> **Experimental High-Concurrency Automation Framework (Node.js)**
> **For controlled environments, labs, and research only**

---

## ⚠️ Important Notice

This project is **NOT intended for use against systems you do not own or explicitly have permission to test**.

Running network automation, stress tests, or security experiments against third-party systems **may be illegal** and can result in **criminal or civil penalties**.

**Use this software only in:**

* Localhost / lab environments
* Private infrastructure you own
* Explicitly authorized testing environments

The author and contributors assume **no liability** for misuse.

---

## Overview

**ExtremeAutomation** is a Node.js experimental framework designed to explore:

* High-concurrency networking in Node.js
* Worker Threads and clustering
* Async I/O under load
* Metrics aggregation and logging
* Automation orchestration patterns

The project combines multiple modules into a single class for experimentation and learning purposes.

---

## Features

* ⚙️ Configurable concurrency (`maxWorkers`)
* 🧵 Worker Threads & cluster-style execution
* 🌐 HTTP/HTTPS request automation
* 📊 Runtime statistics tracking
* 📝 JSON and text reporting
* 📂 Target loading from file
* 🪵 Logging with adjustable verbosity

---

## Project Structure

```
.
├── ExtremeAutomation.js
├── targets.txt
├── automation.log
├── output/
│   ├── report-<timestamp>.json
│   └── stats.txt
└── README.md
```

---

## Requirements

* **Node.js v18+** (recommended)
* Linux / macOS (Windows may work with limitations)
* Sufficient file descriptor limits for concurrency tests

Optional (lab use only):

* `sshpass` (not recommended for production or real systems)

---

## Installation

No external npm dependencies are required.

---

## Configuration

Configuration is passed when creating the instance:

```js
const automation = new ExtremeAutomation({
    maxWorkers: 16,
    timeout: 5000,
    retryAttempts: 5,
    logLevel: 'INFO',
    targetFile: 'targets.txt',
    outputDir: './output'
});
```

### Config Options

| Option          | Description                      |
| --------------- | -------------------------------- |
| `maxWorkers`    | Maximum worker threads           |
| `timeout`       | Network timeout (ms)             |
| `retryAttempts` | Retry count (experimental)       |
| `logLevel`      | `DEBUG`, `INFO`, `WARN`, `ERROR` |
| `targetFile`    | File containing targets          |
| `outputDir`     | Output directory for reports     |

---

## Targets File

`targets.txt` example:

```
# Comments are ignored
localhost
127.0.0.1
example.internal
```

Each line represents one target.

---

## Usage

### Basic Initialization

```js
const ExtremeAutomation = require('./ExtremeAutomation');

const automation = new ExtremeAutomation({
    maxWorkers: 8,
    targetFile: 'targets.txt'
});
```

---

### Cluster Mode (Controlled Environments Only)

```js
automation.launchClusterMode(() => {
    console.log('Cluster execution completed');
});
```

This will:

* Spawn worker threads
* Distribute targets
* Collect results
* Export reports

---

## Output

### JSON Report

Saved in `output/report-<timestamp>.json`

Includes:

* Timestamp
* Aggregated statistics
* Results array
* Target count

### Stats File

Saved as `output/stats.txt`

```
Requests: 12345
Successes: 6789
Failures: 4556
```

---

## Logging

Logs are written to:

```
automation.log
```

Log verbosity is controlled via `logLevel`.

---

## Known Limitations

* Async initialization is not awaited (intentional for experimentation)
* Stats aggregation is approximate in clustered mode
* No global rate limiting
* No graceful worker shutdown
* Not production-hardened
* Not audited for security

---

## Intended Use Cases

✅ Acceptable:

* Learning Node.js concurrency
* Load behavior analysis on localhost
* Worker thread experimentation
* Automation framework prototyping
* Defensive tooling research

❌ Not acceptable:

* Attacking public servers
* Unauthorized access attempts
* Denial-of-service testing without permission
* Brute-force attempts on real systems

---

## Disclaimer

This software is provided **“idspaceX1”**, without warranty of any kind.
Use responsibly and legally.

---

## License

**Educational / Research Use Only**
