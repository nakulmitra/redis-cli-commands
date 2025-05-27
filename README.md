# Redis CLI Commands with Theory

Redis (REmote DIctionary Server) is an open-source, in-memory **key-value data store** used as a **database**, **cache**, and **message broker**. It offers high performance and supports various data types like strings, lists, sets, sorted sets, and hashes.

The `redis-cli` is the **command-line interface tool** to interact with the Redis server.

## Theory

* **In-memory**: Fast read/write because data is stored in memory.
* **Key-Value Store**: Every piece of data is stored as a key-value pair.
* **Data Persistence**: Redis can persist data to disk using RDB snapshots or AOF.
* **Use Cases**: Caching, session storage, leaderboard systems, pub/sub, rate limiting.

## Connecting to Redis

```bash
redis-cli              # Connect to default host (localhost:6379)
redis-cli -h <host> -p <port>   # Connect to remote server
redis-cli -a <password>         # If Redis requires authentication
```

## Key Commands

### Set a Key

```bash
SET key value
```

Example:

```bash
SET username devportal
```

### Get a Key

```bash
GET key
```

Example:

```bash
GET username
```

### Delete a Key

```bash
DEL key
```

Example:

```bash
DEL username
```

### Check if Key Exists

```bash
EXISTS key
```

### Set Key with Expiry

```bash
SETEX key seconds value
```

Example:

```bash
SETEX otp 60 "123456"
```

## Expiry & TTL

### Set Expiry on a Key

```bash
EXPIRE key seconds
```

### Get Remaining TTL

```bash
TTL key
```

## Data Structures

### 1. **Strings**

```bash
SET city "New York"
GET city
```

### 2. **Lists**

```bash
LPUSH list1 "a"
RPUSH list1 "b"
LRANGE list1 0 -1
```

### 3. **Sets**

```bash
SADD set1 "apple" "banana"
SMEMBERS set1
```

### 4. **Hashes**

```bash
HSET user:100 name "Prince"
HGET user:100 name
HGETALL user:100
```

### 5. **Sorted Sets**

```bash
ZADD leaderboard 100 "Prince"
ZADD leaderboard 120 "Nakul"
ZRANGE leaderboard 0 -1 WITHSCORES
```

## Authentication

If Redis has a password set:

```bash
AUTH yourpassword
```

## Flush Commands

> Be careful: These will delete data.

```bash
FLUSHDB   # Delete keys in current DB
FLUSHALL  # Delete all keys in all DBs
```

## Server & Info

```bash
INFO              # View server info and stats
DBSIZE            # Number of keys in the current DB
PING              # Check if server is alive
MONITOR           # Real-time command logging
```

## Key Scanning

```bash
KEYS *            # List all keys (not recommended in production)
SCAN 0            # Cursor-based iteration (better than KEYS)
```

## Pub/Sub Example

### Publisher:

```bash
PUBLISH channel1 "Hello World"
```

### Subscriber:

```bash
SUBSCRIBE channel1
```

## Select Redis Database

```bash
SELECT 0       # Redis has DBs numbered 0 - 15 by default
```

## 📌 Summary Table

| Command                 | Description        |
| ----------------------- | ------------------ |
| `SET key val`           | Set a key          |
| `GET key`               | Get a key          |
| `DEL key`               | Delete a key       |
| `EXPIRE key sec`        | Set TTL            |
| `TTL key`               | Get remaining time |
| `HSET` / `HGET`         | Hash operations    |
| `SADD` / `SMEMBERS`     | Set operations     |
| `LPUSH` / `LRANGE`      | List operations    |
| `ZADD` / `ZRANGE`       | Sorted set         |
| `INFO`                  | Server info        |
| `FLUSHALL` / `FLUSHDB`  | Clear data         |
| `MONITOR`               | Live log view      |
| `AUTH`                  | Authenticate       |
| `KEYS *` / `SCAN`       | List keys          |
| `PUBLISH` / `SUBSCRIBE` | Messaging          |