<div align="center">

<img src="https://true-async.github.io/assets/logo-header.png" alt="PHP True Async" height="80">

# PHP True Async

**True Asynchronous inside PHP**

Imagine PHP with coroutines, where familiar functions support concurrent I/O.
No colored `async` functions. Just do `spawn()` and go!

[![Documentation](https://img.shields.io/badge/Docs-true--async.github.io-blue?style=flat-square)](https://true-async.github.io/en/)
[![Download](https://img.shields.io/badge/Download-Install-green?style=flat-square)](https://true-async.github.io/en/download.html)
[![RFC](https://img.shields.io/badge/RFC-php--true--async-orange?style=flat-square)](https://github.com/true-async/php-true-async-rfc)
[![Discord](https://img.shields.io/badge/Discord-Join-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/yqBQPBHKp5)

</div>

---

## What is this?

**PHP True Async** brings native coroutines to the PHP core — no extensions swapping out blocking functions, no framework magic. Regular PHP functions (`fread`, `fwrite`, `curl`, `PDO`, `fsockopen`) become non-blocking automatically inside a coroutine.

```php
$task1 = spawn(function() {
    $pdo = new PDO($dsn);
    $stmt = $pdo->prepare("SELECT * FROM users WHERE id = ?");
    $stmt->execute([1]);       // non-blocking I/O, yields to other coroutines
    return $stmt->fetch();
});

$task2 = spawn(function() {
    $socket = fsockopen($host, 9000);
    fwrite($socket, "ping");   // non-blocking, runs concurrently with $task1
});
```

## Project Structure

| Repository | Description |
|---|---|
| [php-src `true-async`](https://github.com/true-async/php-src/tree/true-async-stable) | PHP core with TrueAsync API + coroutine scheduler |
| [php-async](https://github.com/true-async/php-async) | Extension implementing the TrueAsync API (libuv reactor) |
| [php-true-async-rfc](https://github.com/true-async/php-true-async-rfc) | RFC, design documents and rationale |
| [releases](https://github.com/true-async/releases) | Pre-built binaries for Linux, macOS and Windows |

## Get Started

Full installation instructions for Linux, macOS, Windows and Docker:
**[→ Download & Install](https://true-async.github.io/en/download.html)**

Full API reference and guides:
**[→ Documentation](https://true-async.github.io/en/)**

## Contributing

We welcome contributions of all kinds — code, docs, testing, and community support.
**[→ Contributing Guide](https://true-async.github.io/en/contributing.html)**

---

<div align="center">

💬 [Discord](https://discord.gg/yqBQPBHKp5) · 📖 [Docs](https://true-async.github.io/en/) · 🐛 [Issues](https://github.com/true-async/php-async/issues)

</div>
