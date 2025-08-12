# Python Programming 

***

## 1. What Python is Used For

**Domains:**
- **Web Development**: Django, Flask, FastAPI.
- **Data Science / AI / ML**: NumPy, Pandas, Matplotlib, SciPy, Scikit-Learn, TensorFlow, Keras, PyTorch.
- **Automation / DevOps**: CLI tools, AWS SDK (`boto3`), Google Cloud SDK, Ansible modules.
- **Web Scraping**: BeautifulSoup, Scrapy, Selenium.
- **Scripting & Utilities**: Backup scripts, CI/CD pipelines, cronjob management, monitoring tools.

***

## 2. Environment Setup

**Install Python:**
```sh
brew install python
# or use pyenv for multi-version
brew install pyenv
pyenv install 3.11.4
```

**Install IDE:**
- PyCharm, VS Code, or JetBrains Toolbox.
- `which python3` shows interpreter path.

**Virtual Environments (best practice):**
```sh
python3 -m venv venv
source venv/bin/activate
```

***

## 3. Python Fundamentals

### Data Types
- Strings: `"string"` or `'string'`
- Integers, Floats
- Booleans: `True`, `False`
- Containers: list, tuple, set, dict

### Variables
- Dynamic typing, snake_case naming.

```python
seconds_per_day = 24 * 60 * 60
```

### Functions
```python
def days_to_units(days, unit="seconds"):
    FACTORS = {"seconds": 86400, "minutes": 1440}
    return f"{days} days = {days * FACTORS[unit]} {unit}"
```

***

## 4. Control Flow & Error Handling

```python
try:
    value = int(input("Enter a value: "))
    if value  requirements.txt
pip install -r requirements.txt
```

***

## 10. Object-Oriented Programming (OOP)

```python
class User:
    def __init__(self, email, name):
        self.email = email
        self.name = name
    def greet(self):
        print(f"Hi, {self.name}")
```

- Encapsulation: `_protected`, `__private`.
- Inheritance:
```python
class Admin(User):
    def greet(self):
        super().greet()
        print("Admin privileges enabled")
```
- **Dataclasses**:
```python
from dataclasses import dataclass
@dataclass
class Point:
    x: int
    y: int
```

***

## 11. **Advanced Python Features** (Deep Dive)

### Decorators
- **Function Decorator**: Higher-order function modifying another function.
```python
def log_call(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

@log_call
def add(a, b):
    return a + b
```
- **Class Decorator**:
```python
def singleton(cls):
    instances = {}
    def get_instance(*args, **kwargs):
        if cls not in instances:
            instances[cls] = cls(*args, **kwargs)
        return instances[cls]
    return get_instance
```

### Iterators & Generators
```python
def my_gen():
    for i in range(3):
        yield i

g = my_gen()
next(g)
```

### Context Managers
```python
class ManagedFile:
    def __enter__(self):
        self.file = open("log.txt", "w")
        return self.file
    def __exit__(self, exc_type, exc_val, exc_tb):
        self.file.close()

with ManagedFile() as f:
    f.write("Hello")
```
Or use `contextlib`:
```python
from contextlib import contextmanager
@contextmanager
def open_file(name):
    f = open(name)
    try:
        yield f
    finally:
        f.close()
```

### Metaclasses
- Control class creation.
```python
class Meta(type):
    def __new__(cls, name, bases, attrs):
        attrs['created_by_metaclass'] = True
        return super().__new__(cls, name, bases, attrs)

class MyClass(metaclass=Meta):
    pass
```

### Descriptors
- Control attribute access.
```python
class Descriptor:
    def __get__(self, obj, objtype=None): ...
    def __set__(self, obj, value): ...
```

***

## 12. Functional Programming Tools

- `map`, `filter`, `reduce`, `zip`
- `functools.lru_cache` for memoization
- `itertools` for combinatorics, lazy iterables.

***

## 13. Type Hints and Static Typing

```python
def greet(name: str) -> str:
    return f"Hello {name}"
```
Run `mypy` for static type checking.

***

## 14. Concurrency & Parallelism

- `threading` for IO-bound
- `multiprocessing` for CPU-bound
- `asyncio` for async/await tasks.

***

## 15. Testing

- `unittest` built-in
- `pytest` for advanced fixtures, parametrization.

***

## 16. Best Practices

- Follow **PEP8** style guide.
- Use `black` for formatting, `flake8`/`pylint` for linting.
- Isolate deps via `venv` or `poetry`.

***

### 🔹 Key Takeaways
- Python is versatile for scripting, DevOps, web, and AI.
- Learn **advanced patterns** (decorators, context managers, metaclasses).
- Combine OOP with functional tools.
- Use type hints & testing for large systems.
- Automate with Python in CI/CD pipelines, cloud APIs, and infrastructure scripts.

***

**Python Advanced Recipes** file containing **ready‑to‑use patterns for decorators, metaclasses, context managers, and async utilities** — all geared towards practical DevOps automation use cases.

***

```python
"""
Python Advanced Recipes for DevOps Automation
---------------------------------------------
This module contains reusable code snippets for:
- Decorator patterns (logging, retries, timing, permissions)
- Metaclass customization
- Context manager tricks (resource management, temp files, remote connections)
- Async patterns (parallel API calls, async command execution)
"""

import functools
import time
import logging
import os
from contextlib import contextmanager
import tempfile
import shutil
import asyncio
import aiohttp
from subprocess import CalledProcessError, run


# -------------------------------------------------
# 1. DECORATORS
# -------------------------------------------------

def log_call(func):
    """Log function calls with args for auditing."""
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        logging.info(f"[CALL] {func.__name__} args={args}, kwargs={kwargs}")
        return func(*args, **kwargs)
    return wrapper


def retry_on_exception(retries=3, delay=2, exceptions=(Exception,)):
    """Retry a function call on specified exceptions (for flaky network cmds)."""
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            last_err = None
            for attempt in range(1, retries + 1):
                try:
                    return func(*args, **kwargs)
                except exceptions as e:
                    logging.warning(f"Attempt {attempt} failed: {e}")
                    last_err = e
                    time.sleep(delay)
            raise last_err
        return wrapper
    return decorator


def time_it(func):
    """Measure execution time of the function."""
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        start = time.perf_counter()
        result = func(*args, **kwargs)
        elapsed = time.perf_counter() - start
        logging.info(f"[TIME] {func.__name__} executed in {elapsed:.2f}s")
        return result
    return wrapper


# Example usage:
@log_call
@retry_on_exception(retries=5, delay=1)
@time_it
def flaky_network_task(url):
    """Simulate network call (replace with actual API call)."""
    if time.time() % 2 < 1:
        raise ConnectionError("Simulated network failure")
    return f"Fetched data from {url}"


# -------------------------------------------------
# 2. METACLASS EXAMPLES
# -------------------------------------------------

class AutoRegister(type):
    """Automatically register subclasses (e.g., for plugins)."""
    registry = {}

    def __init__(cls, name, bases, attrs):
        if not name.startswith("Base"):
            AutoRegister.registry[name] = cls
        super().__init__(name, bases, attrs)


class BaseTask(metaclass=AutoRegister):
    """Base class for all tasks."""
    pass


class BackupTask(BaseTask):
    def run(self):
        print("Running backup...")


class CleanupTask(BaseTask):
    def run(self):
        print("Cleaning up old resources...")


# -------------------------------------------------
# 3. CONTEXT MANAGER TRICKS
# -------------------------------------------------

@contextmanager
def temp_directory():
    """Create a temporary directory, cleanup automatically."""
    dirpath = tempfile.mkdtemp()
    try:
        yield dirpath
    finally:
        shutil.rmtree(dirpath)


@contextmanager
def change_dir(path):
    """Temporarily change working directory."""
    prev_cwd = os.getcwd()
    os.chdir(path)
    try:
        yield
    finally:
        os.chdir(prev_cwd)


class SSHConnection:
    """Context Manager for SSH connections."""
    def __init__(self, host, user):
        self.host = host
        self.user = user

    def __enter__(self):
        logging.info(f"Opening SSH connection to {self.user}@{self.host}")
        # Here you could initialize a paramiko SSHClient or similar
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        logging.info(f"Closing SSH connection to {self.user}@{self.host}")
        # Clean up connection if needed


# -------------------------------------------------
# 4. ASYNC PATTERNS (DEVOPS AUTOMATION)
# -------------------------------------------------

async def async_shell(cmd):
    """Run shell command asynchronously."""
    proc = await asyncio.create_subprocess_shell(
        cmd, stdout=asyncio.subprocess.PIPE, stderr=asyncio.subprocess.PIPE
    )
    stdout, stderr = await proc.communicate()
    if proc.returncode != 0:
        raise CalledProcessError(proc.returncode, cmd, stderr)
    return stdout.decode().strip()


async def fetch_url(session, url):
    """Fetch JSON data from a URL asynchronously."""
    async with session.get(url) as resp:
        resp.raise_for_status()
        return await resp.json()


async def parallel_fetch(urls):
    """Fetch multiple URLs in parallel."""
    async with aiohttp.ClientSession() as session:
        tasks = [fetch_url(session, u) for u in urls]
        return await asyncio.gather(*tasks)


# -------------------------------------------------
# 5. IF RUN AS SCRIPT → DEMO
# -------------------------------------------------

if __name__ == "__main__":
    logging.basicConfig(level=logging.INFO)

    # Decorator demo
    try:
        print(flaky_network_task("https://example.com"))
    except Exception as e:
        print(f"Final failure: {e}")

    # Metaclass demo
    print("Registered Tasks:", AutoRegister.registry)
    for task_cls in AutoRegister.registry.values():
        task_cls().run()

    # Context managers demo
    with temp_directory() as tmp:
        print(f"Using temp dir: {tmp}")

    # Async demo
    urls = ["https://api.github.com", "https://httpbin.org/get"]
    results = asyncio.run(parallel_fetch(urls))
    print(results)
```

***

