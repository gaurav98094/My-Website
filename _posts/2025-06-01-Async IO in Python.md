---
layout: post
title: "Async IO in Python: A Complete Walkthrough"
date: 2025-06-01
categories: [blog]
tags: [python]
description: "Async IO allows you to run code that waits (like for file or network operations) without blocking other tasks, enabling concurrent execution in a single thread using async and await."
---

# Async IO in Python



## **Overview**


When you want a program to do multiple things at once (like downloading a file while processing user input), you need **concurrent programming** tools. There are **three main approaches**:


### 1. **Multiprocessing** (🏋️ CPU-bound tasks)

* **What it is:** Runs tasks in **parallel** using **multiple CPU cores**.
* **Best for:** Heavy computations, number crunching.
* **Example:** Image processing, matrix multiplications.


### 2. **Threading** (📞 IO-bound tasks)

* **What it is:** Runs tasks **concurrently** using multiple threads in a **single process**.
* **Best for:** Tasks that **wait a lot** (like reading files, making API calls).
* **Downside in Python:** The **GIL** (Global Interpreter Lock) limits true parallel execution.


### 3. **Async IO** (⚡ IO-bound tasks, modern way)

* **What it is:** A **single-threaded**, **single-process** model that uses **cooperative multitasking**.
* **Best for:** High-level IO tasks (like handling many web requests).
* **How it works:** Tasks can **"pause" (await)** when waiting for IO and **let others run**.
* **Feels concurrent,** but everything happens in a controlled, non-parallel way.
* **Powered by:** **async** / **await** keywords and the **asyncio** library in Python.


### ✅ Summary Table
<img src="{{ '/images/asyncio1.png' | relative_url }}">

---

## **Asyncio Package**
Asyncio is  library in Python (since version 3.4) for writing asynchronous programs—especially those that deal with IO-bound tasks like web servers, APIs, or any program that waits on external systems. It has two keywords **async** and **await** that serve diiferent purpose but come together to help you declare, build, execute and manage asyncronous programming.


### 🧩 How they work together:

* Think of **async** and **await** as the **building blocks**.

  * **async** lets you **define** an asynchronous function (called a *coroutine*).
  * **await** lets you **pause** the function until another asynchronous operation finishes.

* Think of **asyncio** as the **orchestrator**.

  * It provides tools like **event loops**, **tasks**, and **schedulers** to **run and manage** the async code you've written using **async** and **await**.

---

### 🔄 Scenario:

Let's simulate an IO-bound task, like **fetching data from a server**, where we just sleep for a few seconds to mimic delay.

```python
import asyncio

# Define an async function (a coroutine)
async def fetch_data(id):
    print(f"Start fetching data for task {id}...")
    await asyncio.sleep(2)  # Simulates IO (like API call, file read)
    print(f"Finished fetching data for task {id}")
    return f"Data {id}"

# Main function to run multiple coroutines concurrently
async def main():
    # Run three fetch tasks concurrently using asyncio.gather
    results = await asyncio.gather(
        fetch_data(1),
        fetch_data(2),
        fetch_data(3)
    )
    print("Results:", results)

# Run the event loop
asyncio.run(main())
```



### 🧠 What's Happening Here:

* **async def** defines a coroutine: **fetch_data** and **main**.
* **await** tells Python to **pause** that coroutine and let other coroutines run.
* **asyncio.gather(...)** runs multiple coroutines **concurrently**.
* **asyncio.run(...)** starts the **event loop**, which coordinates all async tasks.


### 🕐 Output:

```
Start fetching data for task 1...
Start fetching data for task 2...
Start fetching data for task 3...
Finished fetching data for task 1
Finished fetching data for task 2
Finished fetching data for task 3
Results: ['Data 1', 'Data 2', 'Data 3']
```

Even though each task takes 2 seconds, they run **at the same time**, so the total time is 2 seconds instead of 6.


Here's a clearer and simpler version of the explanation:

---

## **Async IO Rule**

Let's break down the basics of <i>async</i>, <i>await</i>, and coroutine functions. These concepts might feel a bit tricky at first, but they're very important. Don't worry if it doesn't click right away—feel free to revisit this section as needed.

#### 1. <i>async def</i>

When you define a function using <i>async def</i>, you're creating a **coroutine**. Coroutines are special functions that can pause and resume their execution. They are used for writing asynchronous code.

Example:

```python
async def my_coroutine():
    ...
```

#### 2. <i>await</i>

The keyword <i>await</i> is used **inside an async function** to pause its execution until the result of another async function is ready. It tells Python:
"Pause this function here, and let other code run in the meantime. Come back when the awaited task is done."

Example:

```python
await some_async_function()
```

This is how **await** hands control back to the **event loop**, which then looks for other tasks to run while it waits.


### Important Rules About Using async and await

There are some strict rules about when and how you can use <i>async</i> and <i>await</i>. Knowing these will help you avoid common mistakes, whether you're just learning or already familiar with async programming.

1. **async def creates a coroutine function**
   When you write a function with <i>async def</i>, it becomes a coroutine. Inside this function, you **can** use <i>await</i>, <i>return</i>, or <i>yield</i>, but none of these are required.
   For example, this is valid even though it does nothing:

   ```python
   async def noop():
       pass
   ```

2. **Calling coroutine functions requires <i>await</i>**
   If a coroutine function uses <i>await</i> or <i>return</i>, you must **await** it to get the result:

   ```python
   result = await my_coroutine()
   ```

3. **<i>yield</i> inside <i>async def</i> creates an asynchronous generator**
   This is a newer feature in Python. Using <i>yield</i> in an <i>async def</i> function makes it an **asynchronous generator**. You loop over this using <i>async for</i>.
   But don't worry about async generators right now — focus first on understanding normal coroutine functions that use <i>await</i> and <i>return</i>.

```python
import asyncio

# 1. async def creates a coroutine function — this one does nothing (like noop)
async def noop():
    pass

# 2. async def with await and return — you must await it to get the result
async def greet():
    await asyncio.sleep(1)  # simulate async operation (like waiting)
    return "Hello, async!"

# 3. async def with yield — creates an async generator
async def async_counter():
    for i in range(3):
        await asyncio.sleep(0.5)  # simulate async operation
        yield i

async def main():
    await noop()  # calling coroutine function with no await inside

    message = await greet()  # await is needed to get the return value
    print(message)

    # async for to iterate over async generator
    async for number in async_counter():
        print(f"Count: {number}")

asyncio.run(main())
```


## **Asynchronous Image Downloader**

```python
#!/usr/bin/env python3
# download_images.py

"""
Asynchronously download multiple images from a list of URLs and save them to disk.

This script demonstrates the power of asyncio + aiohttp + aiofiles for
concurrent I/O-bound tasks like downloading files from the internet.

---

Features:
- Reads image URLs from a file
- Downloads all images concurrently using asyncio
- Saves images locally with proper filenames
- Logs progress for visibility

Ideal for:
- Async programming learners
- Web scraping / automation scripts
- Efficient batch downloads

Author: Your Name
Date: 2025-06-02
"""

import asyncio
import aiohttp
import aiofiles
import pathlib
import logging
from aiohttp import ClientSession

# --- Configuration ---

# Folder to save downloaded images
IMAGE_DIR = pathlib.Path("images")
IMAGE_DIR.mkdir(exist_ok=True)

# Input and Output files
URLS_FILE = pathlib.Path("image_urls.txt")
LOG_FILE = pathlib.Path("download_log.txt")

# --- Logging Setup ---

logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s [%(levelname)s] %(message)s",
    handlers=[
        logging.StreamHandler(),
        logging.FileHandler(LOG_FILE, mode="w")
    ]
)
logger = logging.getLogger("image_downloader")

# --- Core Async Functions ---

async def download_image(session: ClientSession, url: str, index: int) -> None:
    """
    Download an image from the given URL and save it to disk.

    Args:
        session (ClientSession): An aiohttp session for making requests.
        url (str): The image URL to download.
        index (int): An index for naming the downloaded file.

    Raises:
        Logs error if download or file write fails.
    """
    try:
        async with session.get(url) as response:
            response.raise_for_status()
            data = await response.read()
            file_path = IMAGE_DIR / f"image_{index}.jpg"

            async with aiofiles.open(file_path, mode="wb") as f:
                await f.write(data)

            logger.info(f"✅ Downloaded: {url} -> {file_path}")
    except Exception as e:
        logger.error(f"❌ Failed to download {url}: {e}")

async def bulk_download_images(urls: list[str]) -> None:
    """
    Download multiple images concurrently.

    Args:
        urls (list[str]): List of image URLs to download.
    """
    async with aiohttp.ClientSession() as session:
        tasks = [
            download_image(session, url, i)
            for i, url in enumerate(urls)
        ]
        await asyncio.gather(*tasks)

# --- Entry Point ---

def load_urls(file_path: pathlib.Path) -> list[str]:
    """Load image URLs from a text file."""
    with open(file_path, "r") as f:
        return [line.strip() for line in f if line.strip()]

if __name__ == "__main__":
    # Validate Python version
    import sys
    assert sys.version_info >= (3, 7), "Python 3.7+ required."

    # Load URLs from file
    if not URLS_FILE.exists():
        logger.error(f"URL list file not found: {URLS_FILE}")
        sys.exit(1)

    urls = load_urls(URLS_FILE)
    logger.info(f"Found {len(urls)} URLs to download.")

    # Start event loop
    asyncio.run(bulk_download_images(urls))
    logger.info("All downloads completed.")
```

### 📥 Sample <i>image_urls.txt</i>

```
https://via.placeholder.com/150
https://via.placeholder.com/200
https://via.placeholder.com/250
https://via.placeholder.com/300
```

## **Conclusion**

You’ve learned how Python’s <i>async</i>, <i>await</i> and the <i>asyncio</i> library enable efficient, non-blocking concurrency for I/O-bound tasks. By using coroutines and event loops, you can write clean, scalable code — perfect for tasks like downloading files, web scraping, or handling many network requests at once.


