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
   ./configure --enable-experimental-async-api --enable-async
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
   configure --enable-experimental-async-api --enable-async
   nmake
   ```

## Contacts

💬 [Discord Discussions](https://discord.gg/94xcsfSR)

---

**PHP TRUE ASYNC** — making async a standard in PHP!
