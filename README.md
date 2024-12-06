<div align="center">
  <img width="100" height="100" src="https://avatars.githubusercontent.com/u/190339082" >
  <h2>𐬺 TinyO</h2>
  <h5>Next level orchestration.</h5>
  <p align="center">
    <a href="#vision"><b>Why</b></a> •
    <a href="#quickstart"><b>Quickstart</b></a> •
    <a href="https://discord.gg/ERKBk6ArnQ" target="_blank"><b>Discord</b></a> •
    <a href="https://x.com/PureLinux" target="_blank">𝕏</a>
  </p>
</div>

**TIO** - An extremely **simple** cloud-native container **orchestrator** that is trying to be a [Rust][rust-lang.org] alternative to more complex solutions like [K8s][kubernetes.io] ([Golang][go.dev]).

<blockquote>
 <span>
    It's tiny, but it's fast.
 </span>
</blockquote>

It's currently in an early **alpha** state.
We're working on the first safe single node **localhost version** for **Linux®** & **MacOS®**.

<blockquote>
 <span>
    TIO tries to tackle known K8s complexities.
 </span>
</blockquote>

Check out the [k8s/complexities.md][repo-docs-vision-comparisons-k8s-complexities.md] for an overview of the challenges we want to address, among others.
<br/>
<br/>

### 💥 Challenge

If you're able to delete lines and/or break the [runtime][tinyort] in any meaningful way you will be listed below (<a href="#code-wizards">Code Wizards</a>). Please be kind, this is an early alpha.

<blockquote>
 <span>
    If you can break it, you truly understand it.
 </span>
</blockquote>
<br/>

Please give the **community feedback** about your opinion regarding the development of TIO ([Issues][repo-issues]/[Commits][repo-commits]/[Discussions][repo-discussions]).

Feel free to [![pure-linux-discord](https://img.shields.io/badge/discord-join-7289DA.svg?logo=discord&longCache=true&style=flat)](https://discord.gg/ERKBk6ArnQ).

## Quickstart

Just execute & you're ready to orchestrate on any platform (coming soon). This automatically **installs** ```tinyoctl``` & **initializes** a local **cluster** on the host system. **Be ready in seconds**:

```bash
sh curl tinyo.io/get | bash
```

⚠️ The current alpha version of TIO should only be used in a controlled environment, such as a **virtual machine** (or container, but currently not supported) to prevent **unintended side effects** on your **host system**.

Running TIO **requires root** due to the use of **Linux® namespaces**, pivot_root, mounting filesystems, modifying network interfaces and so on.
Ensure you have the necessary permissions and understand the **security implications** before using TIO Alpha.

## Usage

<blockquote>
 <span>
    We try to achieve more with less.
 </span>
</blockquote>

TIO uses **minimal Statefiles** (```yml```) which are managed via [tinyoctl][tinyoctl] cli.

First **setup** the first cluster **node** via ```tinyoctl``` cli (alias **tio**) by providing a network name, username & password of your initial admin user:
```sh
tio ++ -net [network_name] -u [admin_username] -p [admin_password]
```

To **add** more **nodes** just execute the command above on a different host system with the following ```tinyoctl``` flag in addition:
```sh
-ip [IP of any other existing node]
```

To **isolate containers** just **create** additional **clusters**. A container has **network access** to **any** other container in one cluster.

Here is an **example** to create 1 container with 1 port & 2 mounts:

```sh
tio + alpine-1.yml
```

```yaml
# Source: https://github.com/pure-linux/tinyoctl/blob/release/alpha/0.0.1/examples/basic/alpine-1.yml
container: "alpine:latest"
port: 8080
mounts:
  - source: "/etc/hosts"
    target: "/mnt/hosts"
  - source: "/tmp/local-config"
    target: "/config"
```

## Architecture

<blockquote>
 <span>
    In a nutshell TIO is just an orchestration of runtimes.
 </span>
</blockquote>

The system has the following **3 main components**. [tinyoctl][tinyoctl] interacts with [tinyonode][tinyonode] to start [tinyort][tinyort].
Don't worry about master/worker nodes and so on. The system operates similarly to a **mesh** topology:

- [tinyoctl][tinyoctl]: Contains cli and packages intended for use by client programs.
- [tinyonode][tinyonode]: Controller for each cluster node. Think of it as biolerplate code which is orchestrating the [runtime][tinyort](s).
- [tinyort][tinyort]: Container runtime ([Core Architecture][tinyort-docs-utils-core-readme.md])

E.g. the [tinyort/src/utils/core.rs][tinyort-src-utils-core.rs] currently has the size of about **350** code lines. The **MVP** should remain **below 2-3k** lines for single localhost container with storage & networking (+ Docker Hub download, ..).

To improve TIO and to make it completely accessible to the entire developer community, we introduced the following **3 additional components**:

- [tinyoapt][tinyoapt]: Advanced Package Tool to simplify the setup of various applications within a cluster.
- [tinyodash][tinyodash]: TIO Pro Dashboard for local development & cloud operations.
- [tinyort-fuzzer][tinyort-fuzzer]: Partial automated Fuzzer for the TIO [container runtime][tinyort].

### Unique Runtime Features

#### Optimized Intra-Host Container Communication

TIO introduces an innovative feature for optimizing container communication on the same host, reducing overhead and improving performance. Unlike traditional networking approaches that rely on full TCP/IP stacks or ingress mechanisms, this runtime leverages direct communication methods tailored for Linux architectures.

##### Key Features
- **Unix Domain Sockets (UDS)**: Enables fast and efficient inter-container communication without the overhead of TCP/IP. Each container communicates via UDS managed by the runtime.
- **Shared Memory (shm)**: Facilitates low-latency data exchange by sharing memory regions between containers for intensive data transfers.
- **Kernel Bypass with eBPF**: Utilizes eBPF for advanced packet routing and filtering, optimizing host-level communication pipelines.
- **Direct Process Piping**: Supports lightweight communication using POSIX pipes for simpler IPC requirements.

##### Benefits

- **Performance Boost**: Drastically reduces network latency and overhead compared to standard container networking.
- **Secure Isolation**: Maintains strict namespace isolation and access control to ensure container security.
- **Customizability**: Designed for flexible implementation to fit diverse container workloads.

## Roadmap

### Phase 1: Solve localhost environment

- Minimal prototype
  - Start alpine container **faster** than **Docker** with low-level libraries
- Base version
  - WIP

## Vision

<blockquote>
 <span>
    Developers want simple, but highly effective tools that reduce (local) infrastructure complexity.
 </span>
</blockquote>

### Comparisons

#### General

- RAM/Memory bandwith is expensive. If we're Rust + tiny this could reduce cloud costs in general.

#### Docker Desktop

- **Speed**: Be faster. (Container/TIO App startup, tinyoctl execution, WIP)
- **Accessibility**: Better GUI (lean, clean & fancy)
- WIP

#### Kubernetes

We aim to **simplify** known K8s difficulties step by step.
To take a look at the most known challenges **jump to [k8s/complexities.md][repo-docs-vision-comparisons-k8s-complexities.md]**.

The goal is to **support important use cases** & **workflows** for which K8s is often used today.

- **Config**: Minimal Statefiles (start with one config line if wanted)
- **Local development**: Start your local containers easily (Quick Quickstart)
- **Cluster topology**: Just a dynamic mesh. E.g. no master & worker network entities.
- **Upgrades**: Hustle free (simple specs -> better LTS compatibility)
- **Scaling**: Infinite (Network mesh entities)
- **Recursive**: Cluster in cluster per default (backup/restore whole clusters easily within a cluster)
- **Speed**: Fast (Rust & low-level libs, achieving lowest container startup times)
- **Efficiency**: More RAM/IO efficient than K8s for similar tasks (less cloud costs)
- **Security**: More stable runtime security
- **Dynamicity**: etcd limitations
- **Monitoring**: Best possible dashboard (visualizations) (E.g.: [k8svisual/vpk](https://github.com/k8svisual/vpk), WIP)
- WIP

---

## PureLinux DAO

All IP (Code, ..) of PureLinux is owned by the [DAO][pure-linux-dao] and the [DAO][pure-linux-dao] is owned by the [contributors][repo-contributors] of the [DAO][pure-linux-dao].

<blockquote>
 <span>
   We think that every contributor should have their fair stake within the projects. Most important for us is that barrier to contribution is as low as possible.
 </span>
</blockquote>

The project development is still very new, feel free to [![pure-linux-discord](https://img.shields.io/badge/discord-join-7289DA.svg?logo=discord&longCache=true&style=flat)](https://discord.gg/ERKBk6ArnQ) for **open discussions** about container orchestration and so on.
We try to **scale** the **development** **with** the **community** so that the project achieves optimal momentum.
Because the **codebase** is in general relatively **small**, one doesn't have to dive too deep into prebuilt structures to make valuable contributions.
We try to give **best possible credit to every contributor** who's bringing this project to the world.

### Process for Stake Distribution

<blockquote>
 <span>
   It's not good for a project when someone digs themselves into a rabbit hole alone, because it makes it harder for others to join or contribute later.
 </span>
</blockquote>

At PureLinux, we try hard to build a decentralized autonomous organization to redefine how open-source **contributions** are **rewarded** and **governed**. We find this very important for the project to grow perfectly.
For every **contribution**, each contributor receives **tokens** for the [DAO][pure-linux-dao], increasing their **financial stake** and/or **influence** in **polls**, including those shaping PureLinux [Product Roadmaps](#Roadmap) and potential future developments.

<blockquote>
 <span>
   It's not just about how big your seat is; it's more about how high the plane is flying.
 </span>
</blockquote>

Our mission is to create a **community-driven Linux® ecosystem** that ensures fairness, transparency, and accessibility for all [contributors][repo-contributors].
**Key features** of the organization will include:

- **Reward Mechanisms**: Valid contributions are rewarded through a transparent token system, ensuring every contributor receives a fair stake based on their personal efforts.
- **Quadratic Funding**: A funding mechanism that prioritizes community-backed initiatives, amplifying the impact of collective support.
- **Decentralized Governance**: Token holders actively participate in shaping the project's direction through votes, empowering [contributors][repo-contributors] to drive innovation.
- **Low Contribution Barriers**: We aim to make contributions seamless and rewarding, both on GitHub and beyond.

### Monetarization

Somehow the [DAO][pure-linux-dao] needs to finance itself (the world is how it is..). Because of that we plan to implement the following monetarization strategies to pay the development of the open-source version of TIO:

- [Dashboard][tinyodash] Pro (Local/Server) [one-time payment]
- Managed services: [TIO Cloud][tinyocloud] Pro (based on [TIO Runtime][tinyort] Pro) [monthly payment]
- Professional support offering for TIO Pro Services [monthly payment]

### Important IP contributors

- [GitHub username] [IP Summary]

### Financial Sponsors

We are very grateful for every GitHub Sponsor, but ⭐️ helps a lot, too!

- [GitHub username]

### Code Wizards

The people that are listed below made important direct and/or indirect contributions to the vision of TIO. It is very important for us to document any credit regarding our very kind [contributors][repo-contributors] of various kinds and to give them their individual fair stake.

- Maybe you? [![pure-linux-discord](https://img.shields.io/badge/discord-join-7289DA.svg?logo=discord&longCache=true&style=flat)](https://discord.gg/ERKBk6ArnQ)

---

PureLinux | Delivering to the open-source community what matters most.

Linux® is the registered trademark of Linus Torvalds in the U.S. and other countries.

[repo-contributors]: https://github.com/pure-linux/tinyo/graphs/contributors
[repo-issues]: https://github.com/pure-linux/tinyo/issues
[repo-commits]: https://github.com/pure-linux/tinyo/commits
[repo-discussions]: https://github.com/pure-linux/tinyo/discussions
[repo-docs-vision-comparisons-k8s-complexities.md]: https://github.com/pure-linux/tinyo/blob/release/alpha/0.0.1/docs/vision/comparisons/k8s/complexities.md
[pure-linux-discord]: https://discord.gg/ERKBk6ArnQ
[pure-linux-dao]: https://github.com/pure-linux/DAO
[tinyoctl]: https://github.com/pure-linux/tinyoctl
[tinyonode]: https://github.com/pure-linux/tinyonode
[tinyort]: https://github.com/pure-linux/tinyort
[tinyort-fuzzer]: https://github.com/pure-linux/tinyort-fuzzer
[tinyoapt]: https://github.com/pure-linux/tinyoapt
[tinyodash]: https://github.com/pure-linux/tinyodash
[tinyocloud]: https://github.com/pure-linux/tinyocloud
[tinyort-src-utils-core.rs]: https://github.com/pure-linux/tinyort/blob/release/alpha/0.0.1/src/utils/core.rs
[tinyort-docs-utils-core-readme.md]: https://github.com/pure-linux/tinyort/blob/release/alpha/0.0.1/docs/utils/core/README.md
[rust-lang.org]: https://rust-lang.org
[kubernetes.io]: https://kubernetes.io
[go.dev]: https://go.dev