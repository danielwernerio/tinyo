# 𐬺 TinyO

<blockquote>
 <span>
    It's tiny, but it's fast.
 </span>
</blockquote>

**TinyOrchestrator** - A minimal Hybrid Cloud Orchestrator.
It's currently in an early **alpha** state.
We're working on the first safe **single node localhost version** for Linux & MacOS.

Currently about **350** code lines for the [features/runtime/core.rs][src-features-runtime-core.rs].
Feel free to take a look at the [Runtime Core Architecture][docs-runtime-core-readme.md].
Please give the **community feedback** about your opinion regarding the development ([Issues](https://github.com/pure-linux/tinyo/issues)/[Commits](https://github.com/pure-linux/tinyo/commits)/[Discussions](https://github.com/pure-linux/tinyo/discussions)).

**MVP** should remain **below 1k** lines for single localhost container with storage & networking (+ Docker Hub download, ..).

Feel free to [![Discord](https://img.shields.io/badge/discord-join-7289DA.svg?logo=discord&longCache=true&style=flat)](https://discord.gg/ERKBk6ArnQ).

## Quickstart

Just execute & you're ready to orchestrate on any platform (coming soon):
```bash
sh curl tinyo.io/get | bash
```

⚠️ The current alpha version of TinyO should only be used in a controlled environment, such as a **virtual machine** (or container, but currently not supported) to prevent **unintended side effects** on your **host system**.

Running TinyO **requires root** due to the use of **Linux namespaces**, pivot_root, mounting filesystems, modifying network interfaces and so on.
Ensure you have the necessary permissions and understand the **security implications** before using TinyO Alpha.

## Usage

TinyO uses **minimal Statefiles** and operates similarly to a **mesh** topology. Don't worry about master/worker nodes and so on. 
Here is an example with 1 Container, 1 Port & 2 Mounts:

```yaml
container: "alpine:latest"
port: 8080
mounts:
  - source: "/etc/hosts"
    target: "/mnt/hosts"
  - source: "/tmp/local-config"
    target: "/config"
```

## Roadmap

##### Phase 1: Solve localhost environment

- Minimal prototype
  - Download & start alpine container **faster** than **Docker** with low-level libs,
configurable via a **minimal Statefile** (`yml`).
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
[src-features-runtime-core.rs]: /src/features/runtime/core.rs
[docs-runtime-core-readme.md]: /docs/runtime/core/README.md