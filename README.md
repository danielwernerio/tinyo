# 𐬺 TinyO

<blockquote>
 <span>
    It's tiny, but it's fast.
 </span>
</blockquote>

**TinyOrchestrator** - A minimal Hybrid Cloud Orchestrator.
It's currently in an early **alpha** state.
We're working on the first safe **single node localhost version** for Linux & MacOS.

Please give the **community feedback** about your opinion regarding the development ([Issues](https://github.com/pure-linux/tinyo/issues)/[Commits](https://github.com/pure-linux/tinyo/commits)/[Discussions](https://github.com/pure-linux/tinyo/discussions)).

<blockquote>
 <span>
    We solve K8s complexities.
 </span>
</blockquote>

Feel free to [![Discord](https://img.shields.io/badge/discord-join-7289DA.svg?logo=discord&longCache=true&style=flat)](https://discord.gg/ERKBk6ArnQ).

## Quickstart

Just execute & you're ready to orchestrate on any platform (coming soon). This automatically **installs** ```tinyoctl``` & **initializes** a local **cluster** on the host system. **Be ready in seconds**:

```bash
sh curl tinyo.io/get | bash
```

<blockquote>
 <span>
    We achieve more with less.
 </span>
</blockquote>

⚠️ The current alpha version of TinyO should only be used in a controlled environment, such as a **virtual machine** (or container, but currently not supported) to prevent **unintended side effects** on your **host system**.

Running TinyO **requires root** due to the use of **Linux namespaces**, pivot_root, mounting filesystems, modifying network interfaces and so on.
Ensure you have the necessary permissions and understand the **security implications** before using TinyO Alpha.

## Usage

TinyO uses **minimal Statefiles** in tandem with [tinyoctl](https://github.com/pure-linux/tinyoctl).

First **setup** the first cluster **node** via ```tinyoctl``` cli (alias **tc**) by providing a network name, username & password of your initial admin user:
```sh
tc ++ -net [network_name] -u [admin_username] -p [admin_password]
```

To **add** more **nodes** just execute the command above on a different host system with the following ```tinyoctl``` flag in addition:
```sh
 -ip [IP of any other existing node]
```

To **isolate containers** just **create** additional **clusters**. A container has **network access** to **any** other container in one cluster.

Here is an **example** to create 1 container with 1 port & 2 mounts:

```sh
tc + examples/basic/alpine-1.yml
```

```yaml
# alpine-1.yml
container: "alpine:latest"
port: 8080
mounts:
  - source: "/etc/hosts"
    target: "/mnt/hosts"
  - source: "/tmp/local-config"
    target: "/config"
```

## Architecture

The system has the following **3 main components**. [tinyoctl](https://github.com/pure-linux/tinyoctl) interacts with [tinyonode](https://github.com/pure-linux/tinyonode) to start [tinyort](https://github.com/pure-linux/tinyort).
Don't worry about master/worker nodes and so on. The system operates similarly to a **mesh** topology:

- [tinyoctl](https://github.com/pure-linux/tinyoctl): Contains cli and packages intended for use by client programs.
- [tinyonode](https://github.com/pure-linux/tinyonode): Controller which is running on every cluster node.
- [tinyort](https://github.com/pure-linux/tinyort): Container runtime ([Core Architecture][tinyort-docs-utils-core-readme.md])

The [tinyort/src/utils/core.rs][tinyort-src-utils-core.rs] currently has the size of about **350** code lines. The **MVP** should remain **below 1k** lines for single localhost container with storage & networking (+ Docker Hub download, ..).

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

#### Docker Desktop

- **Speed**: Be faster. (Container/TinyO App startup, tinyoctl execution, WIP)
- **Accessibility**: Better GUI (lean, clean & fancy)
- WIP

#### Kubernetes

We aim to **simplify** known K8s difficulties step by step.

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
- **Monitoring**: Best possible dashboard visualizations (Inspiration: github.com/k8svisual/vpk)
- WIP

---

## PureLinux DAO

All IP (Code, ..) of PureLinux is owned by the DAO and the DAO is owned by the contributors of the DAO.

<blockquote>
 <span>
   We think that every contributor should have their fair stake within the projects. Most important for us is that barrier to contribution is as low as possible.
 </span>
</blockquote>

The project development is still very new, please feel free to join our [Discord][discord] for **open discussions**.
We try to **scale the development with the community** so that the project achieves optimal momentum.
Because the **codebase** is in general relatively **small**, one doesn't have to dive too deep into prebuilt structures to make valuable contributions.
We try to give **best possible credit to every contributor** who's bringing this project to the world.

<blockquote>
 <span>
   It's not good for a project when someone digs themselves into a rabbit hole alone, because it makes it harder for others to join or contribute later.
 </span>
</blockquote>

At PureLinux, we try hard to build a decentralized autonomous organization to redefine how open-source **contributions** are **rewarded** and **governed**. We find this very important for the project to grow perfectly.

<blockquote>
 <span>
   It's not just about how big your seat is; it's more about how high the plane is flying.
 </span>
</blockquote>

Our mission is to create a **community-driven Linux ecosystem** that ensures fairness, transparency, and accessibility for all contributors.
**Key features** of the organization will include:

- **Reward Mechanisms**: Valid contributions are rewarded through a transparent token system, ensuring every contributor receives a fair stake based on their personal efforts.
- **Quadratic Funding**: A funding mechanism that prioritizes community-backed initiatives, amplifying the impact of collective support.
- **Decentralized Governance**: Token holders actively participate in shaping the project's direction through votes, empowering contributors to drive innovation.
- **Low Contribution Barriers**: We aim to make contributions seamless and rewarding, both on GitHub and beyond.

### Important IP contributors

- [GitHub username] [IP Summary]

### Financial Sponsors

We are very grateful for every GitHub Sponsor, but ⭐️ helps a lot, too!

- [GitHub username]

### Visionaries

The people that are listed here made important direct and/or indirect contributions to the vision of TinyO. It is very important for us to document any credit regarding our very kind contributors of various kinds and to give them their individual fair stake.

- Maybe you? [![Discord](https://img.shields.io/badge/discord-join-7289DA.svg?logo=discord&longCache=true&style=flat)](https://discord.gg/ERKBk6ArnQ)

---

Pure-Linux.com | Delivering to the open-source community what matters most.

[discord]: https://discord.gg/ERKBk6ArnQ
[tinyort-src-utils-core.rs]: https://github.com/pure-linux/tinyort/blob/release/alpha/0.0.1/src/utils/core.rs
[tinyort-docs-utils-core-readme.md]: https://github.com/pure-linux/tinyort/blob/release/alpha/0.0.1/docs/utils/core/README.md