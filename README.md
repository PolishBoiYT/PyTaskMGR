# PyTaskMGR
A Python library that allows you to interact with processes and the system.

## Installation
To install `PyTaskMGR`, you can use `pip`:

```bash
pip install pytaskmgr
```

## Examples:

Terminating a process
```python
from pytaskmgr.process import Process
pid = 69420
image_name = "example.exe"
proc = Process(image_name, pid)
proc.terminate(force=True)
```


Creating a process
```python
from pytaskmgr.process import create_process
proc = create_process("example.exe")
# ...and then you can terminate it that way!
proc.terminate(force=True)
```

Suspending a process (pausing)
```python
from pytaskmgr.process import Process
pid = 69420
image_name = "example.exe"
proc = Process(image_name, pid)
proc.suspend(delay=1, stop=5) # Suspends after 1 second and resumes the process after 5 seconds.
# resume it
proc.resume()
```

Restarting a process
```python
from pytaskmgr.process import Process
pid = 69420
image_name = "example.exe"
proc = Process(image_name, pid)
proc.restart(force=True)
```
or
```python
from pytaskmgr.process import Process
pid = 69420
image_name = "example.exe"
proc = Process(image_name, pid)
proc.terminate(force=True)
create_process(image_name)
# Not recommended because the process might not fully clean its cache or temporary/in-memory files.
```
Getting a process ID by using its name
```python
from pytaskmgr.process import Process
image_name = "example.exe"
proc = Process(image_name)
# Get the process ID
pid = proc.get_pid()
# Returns the process ID (e.g., 69420)
print(pid)
```
Getting a process name by using its ID
```python
from pytaskmgr.process import Process
pid = 69420
proc = Process(pid=pid)
# Get the process ID
image_name = proc.get_image_name()
# Returns the process name (e.g., "example.exe")
print(image_name)
```

# System Related
Getting the amount of RAM
```python
from pytaskmgr.system import System
sys = System()
ram = sys.get_ram()
# Returns the amount of ram in MB (e.g., 8192MB)
print(ram)
# To convert to GB
print(ram.to_gb())
```
Getting the CPU uptime
```python
from pytaskmgr.system import System
sys = System()
cpu = sys.get_cpu()
uptime = cpu.get_uptime()
# Returns the CPU uptime
print(uptime)
```
speaking of CPU...
Getting the CPU Cores
```python
from pytaskmgr.system import System
sys = System()
cpu = sys.get_cpu()
cores = cpu.get_cores()
# Returns the amount of cores (e.g., 4)
print(cores)
```
Getting CPU clock speed
```python
from pytaskmgr.system import System
sys = System()
cpu = sys.get_cpu()
clock_speed = cpu.get_clock_speed()
# Returns the CPU clock speed in MHz (e.g., 3.65 MHz)
print(clock_speed)
```
# Class Explanation

The `Process()` class allows you to interact with a system process by either its image name or PID (Process ID).
Constructor Parameters:

- image_name (str): The name of the process executable (e.g., "example.exe").
- pid (int): The Process ID (e.g., 69420).

The constructor attempts to resolve the process using the following logic:

1. If image_name is valid, it will use that.
2. If image_name is invalid, it will fallback to using pid.
3. If both are invalid, the library will raise an error.

This provides flexibility in managing processes even if you don't know the exact PID of a process.

The `System()` class contains information about your device, what more could you ask for?

# Exceptions
`ProcessNotFound`: Occurs when the process couldn't be found.

`AccessDenied`: Occurs when the user doesn't have permission (by the system) to do harmful things (terminating, restarting the process)

`ProcessCreationFailed`: Occurs when the user tries to create a process, when either its executable is missing or received invalid parameters.

`ProcessRestartFailed`: Occurs when the process failed to restart.

Created by a programmer that sucks at programming, which is *PolishBoiYT!*