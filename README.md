# 𐬺 TinyO

<blockquote>
 <span>
    It's tiny, but it's fast.
 </span>
</blockquote>

This is an early alpha version of the **TinyOrchestrator**.
We're working hard on the first safe **single node localhost version** for **Linux** & **MacOS**.
Feel free to [![Discord](https://img.shields.io/badge/discord-join-7289DA.svg?logo=discord&longCache=true&style=flat)](https://discord.gg/ERKBk6ArnQ).

## Quickstart

Just execute & you're ready to orchestrate on any platform (coming soon):
```bash
sh curl tinyo.io/get | bash
```

⚠️ Use only in a controlled environment, such as a **virtual machine** or container (currently not supported), to prevent **unintended side effects** on your host system.
Running TinyO **requires root** due to the use of namespaces, pivot_root, mounting filesystems, & modifying network interfaces and so on.
Ensure you have the necessary permissions and understand the **security implications** before using this alpha version.

## Usage

TinyO uses **minimal Statefiles**.
Here is an example with 1 Container, 1 Port & 2 Mounts:

```yaml
# Example: 1 Container + 1 Port + 2 Mounts
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
    Developers want simple, but highly effective tools that reduce infrastructure complexity.
 </span>
</blockquote>

## Comparisons

### Docker Desktop

- **Speed**: Be faster (container startup & stuff)
- **Accessibility**: Better GUI (lean & clean)
- WIP

### Kubernetes

We aim to **simplify** known K8s difficulties step by step.
The goal is to **support important use cases** & **workflows**
for which K8s is often used today.

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

## Contribute

The project development is still very new, please join our [Discord][discord] for open discussions.
We try to scale the development with the community so that the project achieves optimal momentum. Because the codebase is relatively small, one doesn't have to dive too deep into prebuilt structures to make valuable contributions.
We try to give best possible credit to every contributor who's bringing this project to the world.

### Sponsors

We are very happy for every GitHub Sponsor, but ⭐️ helps a lot, too!
☑️ Sponsors will be listed in this README.md.

---

Pure-Linux.com | Delivering to the open-source community what matters most.

[discord]: https://discord.gg/ERKBk6ArnQ