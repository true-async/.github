# PHP TRUE ASYNC

**PHP TRUE ASYNC** brings native asynchronous programming to PHP core.

##  Project Structure

### ⚙️ PHP Core

* [true-async](https://github.com/true-async/php-src/tree/true-async-stable) branch — `TrueAsync API` + `PHP` core changes and related libraries
* [true-async-api](https://github.com/true-async/php-src/tree/true-async-api-stable) branch — `TrueAsync API` only

### 🔌 True Async extention

 [`php-async`](https://github.com/true-async/php-async) — Extension implementing the `TrueAsync API`

### 📄 RFC 
[`php-true-async-rfc`](https://github.com/true-async/php-true-async-rfc) — `RFC` and documentation

## Installation

### 🐧 **Unix**

1. **Clone the PHP repository:**

    for example, basic directory name is `php-src`:

   ```
   git clone https://github.com/true-async/php-src -b true-async-api ./php-src
   ```

2. **Clone the `True Async` extension repository:**

    to the `ext` directory of your PHP source:

    ```
    git clone https://github.com/true-async/php-async ./php-src/ext/async
    ```

3. **Install PHP development tools:**

    Make sure you have the necessary development tools installed. On Debian/Ubuntu, you can run:
    
    ```
    sudo apt-get install php-dev build-essential autoconf libtool pkg-config
    ```
    
    For macOS, you can use Homebrew:
    
    ```
    brew install autoconf automake libtool pkg-config
    ```

4. **Install LibUV:**:
   
Please see the [LibUV installation guide](https://github.com/libuv/libuv)

5. **Configure and build:**

   ```
   ./buildconf
   ./configure --enable-async
   make && sudo make install
   ```

   We can use `--enable-debug` to enable debug mode, which is useful for development.

---

### 🖥️ **Windows**

1. **Install php-sdk:**  
   Download and set up [php-sdk](https://wiki.php.net/internals/windows/stepbystepbuild_sdk_2) for building PHP extensions on Windows.

2. **Install and build LibUV:**  
   You can use [vcpkg](https://github.com/microsoft/vcpkg) or build libuv from source.

3. **Copy LibUV files to PHP SDK directories:**

   ```
   1. Copy everything from 'libuv\include' to '%PHP_SDK_PATH%\deps\include\libuv\'
   2. Copy 'libuv.lib' to '%PHP_SDK_PATH%\deps\lib\'
   ```
   `%PHP_SDK_PATH%` is your php-sdk installation root.

4. **Configure and build the extension with PHP:**

   ```
   cd \path\to\php-src
   buildconf
   configure --enable-async
   nmake
   ```

### 🐛 Xdebug
TrueAsync-aware Xdebug 
build: [`true-async/xdebug` `true-async-86` branch](https://github.com/true-async/xdebug/tree/true-async-86).

## 🧟 FrankenPHP

A concurrent coroutine-based server that can handle multiple requests using a single thread:
see: [FrankenPHP with TrueAsync](https://github.com/true-async/frankenphp/tree/true-async)

1. **Build PHP** with async + ZTS + embed (no `=shared`):
   ```bash
   ./configure --prefix=/usr/local --enable-async --enable-zts --enable-embed --with-openssl --with-curl
   make -j$(nproc) && sudo make install
   php-config --configure-options | grep -E "(embed|zts|async)"
   ```
2. **Build FrankenPHP** with TrueAsync tags (sets CGO flags from `php-config`):
   ```bash
   ./build.sh
   # or manually:
   export CGO_CFLAGS="$(php-config --includes)"
   export CGO_LDFLAGS="$(php-config --ldflags) $(php-config --libs)"
   go build -tags "trueasync,nowatcher" -o frankenphp
   ```
3. **Run with Caddy** (async workers get per-thread queues; 503 when buffers are full):
   ```caddyfile
   {
   admin off
   frankenphp {
   # keep defaults for num_threads/max_threads to let FrankenPHP size the pool automatically
   }
   }
   
   :8080 {
   root * /app/www
   
       # Enable PHP server with FrankenPHP
       route {
           # Rewrite all requests to entrypoint.php
           rewrite * /entrypoint.php?uri={http.request.uri.path}
   
           php_server {
               index off
               file_server off
   
               worker {
                   file /app/www/entrypoint.php
                   num 1
                   async
                   buffer_size 20
                   match *
               }
           }
       }
   
       # Logging
       log {
           output file /app/www/storage/logs/frankenphp-access.log
           level INFO
       }
   }
   
   ```

4. Then run `./frankenphp run --config Caddyfile.async` and curl your endpoint.

## Contacts

💬 [Discord Discussions](https://discord.gg/yqBQPBHKp5)

---

**PHP TRUE ASYNC** — making async a standard in PHP!
