<p align="center"> 
  <img src="https://i.imgur.com/PoXC5AA.png" alt="alt logo">
</p>

[![GitHub release](https://img.shields.io/github/release/nxrighthere/BenchmarkNet.svg)](https://github.com/nxrighthere/BenchmarkNet/releases) [![PayPal](https://drive.google.com/uc?id=1OQrtNBVJehNVxgPf6T6yX1wIysz1ElLR)](https://www.paypal.me/nxrighthere) [![Bountysource](https://drive.google.com/uc?id=19QRobscL8Ir2RL489IbVjcw3fULfWS_Q)](https://salt.bountysource.com/checkout/amount?team=nxrighthere) [![Coinbase](https://drive.google.com/uc?id=1LckuF-IAod6xmO9yF-jhTjq1m-4f7cgF)](https://commerce.coinbase.com/checkout/03e11816-b6fc-4e14-b974-29a1d0886697)

_The application is no longer in active public development, all futher work moved to private, this repository turned into read-only mode for historical reference. It was a great experiment, thanks to all supporters and contributors._

BenchmarkNet is a console application for testing the reliable UDP networking solutions.

Features:
- Asynchronous simulation of a large number of clients
- Stable under high-loads
- Simple and flexible simulation setup
- Detailed session information
- Multi-process instances

Supported networking libraries:
- [ENet](https://github.com/nxrighthere/ENet-CSharp "ENet")
- [UNet](https://forum.unity.com/threads/standalone-library-binaries-aka-server-dll.526718 "UNet")
- [LiteNetLib](https://github.com/RevenantX/LiteNetLib "LiteNetLib")
- [Lidgren](https://github.com/lidgren/lidgren-network-gen3 "Lidgren")
- [MiniUDP](https://github.com/ashoulson/MiniUDP "MiniUDP")
- [Hazel](https://github.com/DarkRiftNetworking/Hazel-Networking "Hazel")
- [Photon](https://www.photonengine.com/en/OnPremise "Photon")
- [Neutrino](https://github.com/Claytonious/Neutrino)
- [DarkRift](https://darkriftnetworking.com/DarkRift2)

You can find the latest benchmark results on the [wiki page](https://github.com/nxrighthere/BenchmarkNet/wiki/Benchmark-Results).

How it works?
--------
### Implementation
Each simulated client is one asynchronous task for establishing a connection with the server and processing network events. Each task has one subtask which also works asynchronously to send network messages at a specified interval (15 messages per second by default). So, 1000 simulated clients is 1000 tasks with 1000 subtasks which work independently of each other. This sounds scary, but CPU usage is <1% for tasks itself and every operation is completely thread-safe. The clients send network messages to the server (500 reliable and 1000 unreliable by default). The server also sends messages to the clients in response (48 bytes per message by default). The application will monitor how the data is processed by the server and clients, and report their status in real-time.

### Parallelism degree
TPL automatically performs load-balancing of the coarse-grained tasks with awareness of oversubscription for clients. The server process is running with higher priority to let the operating system make optimal decisions.

Quality control
--------
The application helps to determine many various problems:
- Memory leaks
- Deadlocks
- Buffers exhaustion
- Connections disruption
- GC pressure
- Bugs

Usage
--------
Before launching the application set the desired parameters in the [config file](https://github.com/nxrighthere/BenchmarkNet/wiki/Advanced-Options) to override the default values. Run the application, select the networking library and set any number of simulated clients. Do not perform any actions while the benchmark is running and wait until the process is complete.

When you are going to perform a test with less than 256 simulated clients, it's highly recommended to switch [GC mode](https://github.com/nxrighthere/BenchmarkNet/wiki/Advanced-Options#gc-mode) from Server GC to Workstation GC. You can find more information in [this article](https://blogs.msdn.microsoft.com/seteplia/2017/01/05/understanding-different-gc-modes-with-concurrency-visualizer/) about how different GC modes are working.

You can use any packet sniffer to monitor how the data is transmitted, but it may affect the results.

If you want to simulate a bad network condition, use [Clumsy](http://jagt.github.io/clumsy/ "Clumsy") as an ideal companion.

Discussion
--------
Feel free to join the discussion in the [thread](https://forum.unity.com/threads/benchmarknet-stress-test-for-enet-unet-litenetlib-lidgren-and-miniudp.512507 "thread") on Unity forums.

If you have any questions, contact me via [email](mailto:nxrighthere@gmail.com "email").

Please, check [this](https://github.com/nxrighthere/BenchmarkNet/issues?q=is%3Aissue+is%3Aclosed) section before opening a new issue.

Donations
--------
This project has already had an impact and helped developers in an improvement of the networking libraries. If you like this project, you can support me on [PayPal](https://www.paypal.me/nxrighthere), [Bountysource](https://salt.bountysource.com/checkout/amount?team=nxrighthere) or [Coinbase](https://commerce.coinbase.com/checkout/03e11816-b6fc-4e14-b974-29a1d0886697).

Any support is much appreciated.

Supporters
--------
These wonderful people make open-source better:
<p align="left"> 
  <img src="https://drive.google.com/uc?id=1jVxLviw_CHnjygdfSIdGzLQS2DBdYsa8" alt="supporters">
</p>
