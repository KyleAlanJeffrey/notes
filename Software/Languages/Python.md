Officially managed by Python Software Foundation. See website: https://www.python.org/

Good [video](https://www.youtube.com/watch?v=BkHdmAhapws0)  on how Python works.

## Virtual Environments
Great thread on differences [here](https://stackoverflow.com/questions/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe)

Primary Modules:
- **[`virtualenv`](https://pypi.python.org/pypi/virtualenv)**:  s a very popular tool that creates isolated Python environments for Python libraries. If you're not familiar with this tool, I highly recommend learning it, as it is a very useful tool.
    It works by installing a bunch of files in a directory (eg: `env/`), and then modifying the `PATH` environment variable to prefix it with a custom `bin` directory (eg: `env/bin/`). An exact copy of the `python` or `python3` binary is placed in this directory, but Python is programmed to look for libraries relative to its path first, in the environment directory. It's not part of Python's standard library, but is officially blessed by the PyPA (Python Packaging Authority). Once activated, you can install packages in the virtual environment using `pip`.
    
- `venv`: A package shipped with Python 3, which you can run using `python3 -m venv` (although for some reason some distros separate it out into a separate distro package, such as `python3-venv` on Ubuntu/Debian). It serves the same purpose as `virtualenv`, but only has a subset of its features ([see a comparison here](https://virtualenv.pypa.io/en/latest/)). `virtualenv` continues to be more popular than `venv`, especially since the former supports both Python 2 and 3.

## Package Manager
`PIP` comes standard with Python
Packages can be views at https://pypi.org/

#### PIP Commands

`pip freeze`
List all python packages


## Threading vs Multiprocessing
![[Pasted image 20240410104724.png]]
![[Pasted image 20240410105226.png]]
### Threads
- Python is multithreaded but not simultaneously multithreaded, because of the Global Interpreter Locker (GIL)

![[Pasted image 20240410104849.png]]

- No 2 threads **from the same process** will ever run at the same time.
- To run , the thread must grab the **Global Interpreter Lock**
	- Ensures thready safety
	- Improves single thread performance
	- Bad for multiprocessing


## Asynchronous Programming
**Accomplished with either**
- asyncio
	- Not availible pre python 3.5
- concurrent.futures


Package `asyncio`

**Coroutines**
Any function with `async`. A coroutine is a function that can be suspended and resumed.
A coroutine must be called with an `await coroutine()` or a loop executor.

**Event Loop**
All async code must be run in an event loop. `asyncio.run()` will create an event loop to run code.

**Task**
A coroutine wrapper. Will run any asynchronous function in the background.
Created with `async.create_task()`. Tasks are essentially coroutines that are awaitible
**Pros**
- Can be scheduled concurrently with other tasks
- Can be cancelled
**Pitfalls**
- Calling a blocking function will stop all async execution 


Blocking code can be made non-blocking in python3.9 with asyncio.to_thread(). This will make a thread but add an asyncio interface for the program

The function is not availible in early versions but is simply:
```python
async def to_thread(func, /, *args, **kwargs):
    """Asynchronously run function *func* in a separate thread.
    Any *args and **kwargs supplied for this function are directly passed
    to *func*. Also, the current :class:`contextvars.Context` is propogated,
    allowing context variables from the main thread to be accessed in the
    separate thread.
    Return a coroutine that can be awaited to get the eventual result of *func*.
    """
    loop = events.get_running_loop()
    ctx = contextvars.copy_context()
    func_call = functools.partial(ctx.run, func, *args, **kwargs)
    return await loop.run_in_executor(None, func_call)
```