- **Command injection** -> is the abuse of an application's behaviour to execute commands on the operating system, using the same privileges that the application on a device is running with. It is also known as RCE (*Remote Code Execution*). This exists because applications often use functions in programming languages such as PHP, Python... to pass data and to make system calls on the machine's operating system.
- Blind or verbose command injection.
- `curl`is useful for command injection.
- Dangerous PHP functions -> `exec`, `passthru`, `system`.
- Note: we can bypass a number filter with hexadecimal values.
-  **Command injection CHEAT SHEET** -> https://github.com/payloadbox/command-injection-payload-list

![](./img/ci1.png)
![](./img/ci2.png)
![](./img/ci3.png)
![](./img/ci4.png)
![](./img/ci5.png)
![](./img/ci6.png)
![](./img/ci7.png)
![](./img/ci8.png)
![](./img/ci9.png)
![](./img/ci10.png)
![](./img/ci11.png)