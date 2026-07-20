<div align="center">

![Coretto x Pterodactyl](assets/ptero.png)


<h1>Amazon Corretto for Pterodactyl Panel</h1>

![Java 25](https://img.shields.io/badge/Java-Corretto-orange?style=for-the-badge&logo=openjdk)
![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Pterodactyl](https://img.shields.io/badge/Pterodactyl-Compatible-0e8a16?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

**Optimized Java fork for your Minecraft Server, built by Amazon**

[Quick Start](#-quick-start) • [Installation](#-installation) • [Configuration](#-configuration) • [Flags Optmizaion](#-flags-optimization) • [Documentation](#-documentation)

</div>

---

## Overview

This Docker image provides a production-ready Amazon Corretto environment for Minecraft/Hytale Server.

Ranged from [Java 8 (LTS)](https://www.oracle.com/asean/java/technologies/javase/javase8-archive-downloads.html) to [Java 26](https://www.oracle.com/java/technologies/javase/jdk26-archive-downloads.html), Docker source from [donpedrotv's Java Images list](https://donpedrotv.github.io/pterodactyl-images/#java-amazon-corretto-amd64arm64).

Build with ❤️ by [@ssdarealest](https://alyosha.guru), Head Admin & Developer from [LangBangVN](https://langbangvn.net). [Join the community today!](https://discord.langbangvn.net).

## Features

| Feature                          | Description                                                                                                                                            |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Optimized Java Fork**          | With the power of Amazon Corretto environment, the sky's the limit for your server                                                                     |
| **Long-term enterprise support** | Provides extended, guaranteed security updates and performance enhancements for major Java versions                                                    |
| **Production-tested stability**  | Security patches and critical updates are validated on a massive scale, ensuring they don't introduce performance regressions                          |
| **Zero-cost updates**            | Corretto provides free security patches and bug fixes indefinitely across multiple platforms (Linux, Windows, macOS) without production licensing fees |
| **Game Ready**                   | Designed for Minecraft/Hytale (only with Java 25+), compatible with any Java application                                                               |
| **Lightweight**                  | Only 655 MB with essential dependencies                                                                                                                |
| **Pterodactyl Native**           | Full integration with variable substitution and controls                                                                                               |
| **Auto-Configuration**           | Automatic JAR download and EULA acceptance                                                                                                             |

---

## Quick start

### For server owners

1. **Import the egg** into your Pterodactyl panel:
   - Download `egg-amazon-corretto--universal.json` from this repository
   - Navigate to **Admin Panel** → **Nests** → **Import Egg**
   - Upload the egg file onto the panel & accept import

2. **Create a server**/**Modify startup of a server** using the **Amazon Corretto** egg

3. **Configure and start** your server with your Java 25 application

### For Pterodactyl administrators

```bash
docker pull ssdarealest/corretto-xx-pterodactyl:latest
docker run --rm ssdarealest/corretto-xx-pterodactyl:latest java -version
```

> [!NOTE]
> `xx` define the Java version (ex: `ssdarealest/corretto-26-pterodactyl` for Java 26)

## Installation

### Step 1: Import the Pterodactyl Egg

1. Download the egg configuration file: [`egg-amazon-corretto--universal.json`](egg-amazon-corretto--universal.json)
2. Access your Pterodactyl admin panel
3. Navigate to **Nests** → Select or create a nest
4. Click **Import Egg** and upload the JSON file
5. Configure the Docker image field to your selected version (ex: `ssdarealest/corretto-26-pterodactyl` for Java 26)

### Step 2: Create a Server

1. Go to **Servers** → **Create New Server**
2. Select the **Amazon Corretto** egg → select **your desired Java version**
3. Allocate resources (minimum 2GB RAM recommended)
4. Configure server variables (see [Configuration](#-configuration))

### Step 3: Deploy Your Application

- **Option A**: Provide a direct download URL in `SERVER_JARFILE`
- **Option B**: Upload your JAR file manually to the server directory

---

## Configuration

### Environment Variables

| Variable         | Description                         | Default       | Example                                                                                                                          |
| ---------------- | ----------------------------------- | ------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `SERVER_JARFILE` | Server JAR filename or download URL | `server.jar`  | `https://fill-data.papermc.io/v1/objects/e708e8c132dc143ffd73528cccb9532e2eb17628b1a0eee74469bf466c7003f8/paper-1.21.11-116.jar` |
| `SERVER_MEMORY`  | Memory allocation in MB             | `2048`        | `4096`                                                                                                                           |
| `JAVA_ARGS`      | JVM arguments (see below)           | Aikar's flags | Check out [Flags Optimization](#-flags-optimization) for optimized flags.                                                        |
| `SERVER_ARGS`    | Application-specific arguments      | `nogui`       | `--world-dir /data`                                                                                                              |
| `AUTO_EULA`      | Auto-accept EULA on first start     | `true`        | `false`                                                                                                                          |

---

## Optimized JVM Flags

> [!WARNING]
> These flags usually works on Java 17+. Older Java should use different flags, you can find it out yourself.

The egg comes pre-configured with production-tested JVM flags optimized for game servers:

```bash
-XX:+UseG1GC
-XX:+ParallelRefProcEnabled
-XX:MaxGCPauseMillis=200
-XX:+UnlockExperimentalVMOptions
-XX:+DisableExplicitGC
-XX:+AlwaysPreTouch
-XX:G1HeapWastePercent=5
-XX:G1MixedGCCountTarget=4
-XX:InitiatingHeapOccupancyPercent=15
-XX:G1MixedGCLiveThresholdPercent=90
-XX:G1RSetUpdatingPauseTimePercent=5
-XX:SurvivorRatio=32
-XX:+PerfDisableSharedMem
-XX:MaxTenuringThreshold=1
```

These flags are optimized for:
> - Low latency and reduced GC pauses
> - Efficient memory management
> - High throughput for game servers
> - Tested with Minecraft (compatible with Hytale)
  
I recommend to use these flags, based on your purpose:

- If you are running [LeafMC fork](https://www.leafmc.one/) on Amazon Corretto environment:
```bash
-XX:+UnlockDiagnosticVMOptions -XX:+UnlockExperimentalVMOptions -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:G1HeapRegionSize=16M -XX:G1NewSizePercent=28 -XX:G1MaxNewSizePercent=50 -XX:G1ReservePercent=15 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1SATBBufferEnqueueingThresholdPercent=30 -XX:InitiatingHeapOccupancyPercent=45 -XX:MaxTenuringThreshold=1 -XX:SurvivorRatio=32 -XX:+UseStringDeduplication -XX:+DisableExplicitGC -XX:+UseLargePages -XX:+UseTransparentHugePages -XX:LargePageSizeInBytes=2M -XX:ReservedCodeCacheSize=512M -XX:AllocatePrefetchStyle=3 -XX:+TieredCompilation -XX:TieredStopAtLevel=4 -XX:-DontCompileHugeMethods -XX:MaxNodeLimit=240000 -XX:NodeLimitFudgeFactor=8000 -XX:+OptimizeStringConcat -XX:+PerfDisableSharedMem -Dgale.log.warning.offline.mode=false -Dgale.log.warning.root=false -DGeyser.RakGlobalPacketLimit=100000 -DGeyser.RakPacketLimit=1500 -DGeyser.RakRateLimitingDisabled=true -Djava.awt.headless=true -Djava.net.preferIPv4Stack=true -DLeaf.disable-vanilla-profiler=true -DLeaf.enableFMA=true -Dpaper.explicit-flush=true -Dpaper.playerconnection.keepalive=180 -Dsun.net.maxDatagramSockets=16384 -Dterminal.ansi=true -Dterminal.jline=false
```

- If you are running SMP/large server (flags credited to @MeowIce and [MeowIce's Flags](https://github.com/MeowIce/meowice-flags))

+ **G1CC Version (medium server/below 32GB allocated heap)**
```bash
--add-modules=jdk.incubator.vector -XX:+UseG1GC -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+UnlockDiagnosticVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=28 -XX:G1MaxNewSizePercent=50 -XX:G1HeapRegionSize=16M -XX:G1ReservePercent=15 -XX:G1MixedGCCountTarget=3 -XX:InitiatingHeapOccupancyPercent=20 -XX:G1MixedGCLiveThresholdPercent=90 -XX:SurvivorRatio=32 -XX:G1HeapWastePercent=5 -XX:+PerfDisableSharedMem -XX:G1SATBBufferEnqueueingThresholdPercent=30 -XX:G1ConcMarkStepDurationMillis=5 -XX:G1RSetUpdatingPauseTimePercent=0 -XX:+UseNUMA -XX:-DontCompileHugeMethods -XX:MaxNodeLimit=240000 -XX:NodeLimitFudgeFactor=8000 -XX:ReservedCodeCacheSize=400M -XX:NonNMethodCodeHeapSize=12M -XX:ProfiledCodeHeapSize=194M -XX:NonProfiledCodeHeapSize=194M -XX:NmethodSweepActivity=1 -XX:+UseCriticalJavaThreadPriority -XX:AllocatePrefetchStyle=3 -XX:+AlwaysActAsServerClassMachine -XX:+UseTransparentHugePages -XX:LargePageSizeInBytes=2M -XX:+UseLargePages -XX:+EagerJVMCI -XX:+UseStringDeduplication -XX:+UseAES -XX:+UseAESIntrinsics -XX:+UseFMA -XX:+UseLoopPredicate -XX:+RangeCheckElimination -XX:+OptimizeStringConcat -XX:+UseCompressedOops -XX:+UseThreadPriorities -XX:+OmitStackTraceInFastThrow -XX:+RewriteBytecodes -XX:+RewriteFrequentPairs -XX:+UseFPUForSpilling -XX:+UseFastStosb -XX:+UseNewLongLShift -XX:+UseVectorCmov -XX:+UseXMMForArrayCopy -XX:+UseXmmI2D -XX:+UseXmmI2F -XX:+UseXmmLoadAndClearUpper -XX:+UseXmmRegToRegMoveAll -XX:+EliminateLocks -XX:+DoEscapeAnalysis -XX:+AlignVector -XX:+OptimizeFill -XX:+EnableVectorSupport -XX:+UseCharacterCompareIntrinsics -XX:+UseCopySignIntrinsic -XX:+UseVectorStubs -XX:+UseFastJNIAccessors -XX:+UseInlineCaches -XX:+SegmentedCodeCache -XX:+UseCompactObjectHeaders -Djdk.nio.maxCachedBufferSize=262144 -Djdk.graal.UsePriorityInlining=true -Djdk.graal.Vectorization=true -Djdk.graal.OptDuplication=true -Djdk.graal.DetectInvertedLoopsAsCounted=true -Djdk.graal.LoopInversion=true -Djdk.graal.VectorizeHashes=true -Djdk.graal.EnterprisePartialUnroll=true -Djdk.graal.VectorizeSIMD=true -Djdk.graal.StripMineNonCountedLoops=true -Djdk.graal.SpeculativeGuardMovement=true -Djdk.graal.TuneInlinerExploration=1 -Djdk.graal.LoopRotation=true -Djdk.graal.CompilerConfiguration=enterprise 
```

+ **ZGC (large server/higher than 32GB+ allocated heap)**
> [!WARNING]
> Only use this if you have more than 10 CPU cores; using ZGC on systems with fewer than 8 cores may cause a significant performance impact !
> 
> *credited to @MeowIce and [MeowIce's Flags](https://github.com/MeowIce/meowice-flags)*
```bash
--add-modules=jdk.incubator.vector -XX:+UseZGC -XX:-ZProactive -XX:SoftMaxHeapSize=$((Memory - 2048))M -XX:+UnlockExperimentalVMOptions -XX:+UnlockDiagnosticVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:+PerfDisableSharedMem -XX:+UseNUMA -XX:-DontCompileHugeMethods -XX:MaxNodeLimit=240000 -XX:NodeLimitFudgeFactor=8000 -XX:ReservedCodeCacheSize=400M -XX:NonNMethodCodeHeapSize=12M -XX:ProfiledCodeHeapSize=194M -XX:NonProfiledCodeHeapSize=194M -XX:NmethodSweepActivity=1 -XX:+UseCriticalJavaThreadPriority -XX:AllocatePrefetchStyle=1 -XX:+AlwaysActAsServerClassMachine -XX:+UseTransparentHugePages -XX:LargePageSizeInBytes=2M -XX:+UseLargePages -XX:+EagerJVMCI -XX:+UseStringDeduplication -XX:+UseAES -XX:+UseAESIntrinsics -XX:+UseFMA -XX:+UseLoopPredicate -XX:+RangeCheckElimination -XX:+OptimizeStringConcat -XX:+UseCompressedOops -XX:+UseThreadPriorities -XX:+OmitStackTraceInFastThrow -XX:+RewriteBytecodes -XX:+RewriteFrequentPairs -XX:+UseFPUForSpilling -XX:+UseFastStosb -XX:+UseNewLongLShift -XX:+UseVectorCmov -XX:+UseXMMForArrayCopy -XX:+UseXmmI2D -XX:+UseXmmI2F -XX:+UseXmmLoadAndClearUpper -XX:+UseXmmRegToRegMoveAll -XX:+EliminateLocks -XX:+DoEscapeAnalysis -XX:+AlignVector -XX:+OptimizeFill -XX:+EnableVectorSupport -XX:+UseCharacterCompareIntrinsics -XX:+UseCopySignIntrinsic -XX:+UseVectorStubs -XX:+UseFastJNIAccessors -XX:+UseInlineCaches -XX:+SegmentedCodeCache -XX:+UseCompactObjectHeaders -Djdk.nio.maxCachedBufferSize=262144 -Djdk.graal.UsePriorityInlining=true -Djdk.graal.Vectorization=true -Djdk.graal.OptDuplication=true -Djdk.graal.DetectInvertedLoopsAsCounted=true -Djdk.graal.LoopInversion=true -Djdk.graal.VectorizeHashes=true -Djdk.graal.EnterprisePartialUnroll=true -Djdk.graal.VectorizeSIMD=true -Djdk.graal.StripMineNonCountedLoops=true -Djdk.graal.SpeculativeGuardMovement=true -Djdk.graal.TuneInlinerExploration=1 -Djdk.graal.LoopRotation=true -Djdk.graal.CompilerConfiguration=enterprise
```

---

## Use Cases (referrence from [@janxhg's Java 25 Pterodactyl Egg](https://github.com/ssdarealest/amazon-corretto-pterodactyl))

### Hytale Servers (for Java 25+ only)

```yaml
Server JAR File: https://hytale.com/downloads/server.jar
Server Memory: 4096
Java Arguments: (use default)
Server Arguments: nogui
Auto Accept EULA: true
```

### Custom Java Applications

```yaml
Server JAR File: your-application.jar
Server Memory: 2048
Java Arguments: -Xms2G -Xmx2G -jar
Server Arguments: --config /home/container/config.yml
```

### Modded Servers

```yaml
Server JAR File: https://example.com/modded-server.jar
Server Memory: 8192
Java Arguments: (use default + custom mods flags)
Server Arguments: nogui --forceUpgrade
```

---

## Performance Recommendations

| Server Size    | Players | RAM     | CPU Cores | Storage |
| -------------- | ------- | ------- | --------- | ------- |
| **Small**      | 1-10    | 2-4 GB  | 2         | 10 GB   |
| **Medium**     | 10-50   | 4-8 GB  | 4         | 20 GB   |
| **Large**      | 50-100  | 8-16 GB | 6-8       | 50 GB   |
| **Enterprise** | 100+    | 16+ GB  | 8+        | 100+ GB |

> **Note**: These are general recommendations. Actual requirements will vary based on your specific application, plugins, and world size.

---

## Benchmark

To know if Amazon Corretto works better on Minecraft, I've run two specially Minecraft Server on the same build configuration (400% CPU - Intel E5-2696v3, 8GB RAM), with the same flags config, and here's the result:

> [!NOTE]
> Flags configuration I use:
>
> `-XX:+UnlockDiagnosticVMOptions -XX:+UnlockExperimentalVMOptions -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:G1HeapRegionSize=16M -XX:G1NewSizePercent=28 -XX:G1MaxNewSizePercent=50 -XX:G1ReservePercent=15 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1SATBBufferEnqueueingThresholdPercent=30 -XX:InitiatingHeapOccupancyPercent=45 -XX:MaxTenuringThreshold=1 -XX:SurvivorRatio=32 -XX:+UseStringDeduplication -XX:+DisableExplicitGC -XX:+UseLargePages -XX:+UseTransparentHugePages -XX:LargePageSizeInBytes=2M -XX:ReservedCodeCacheSize=512M -XX:AllocatePrefetchStyle=3 -XX:+TieredCompilation -XX:TieredStopAtLevel=4 -XX:-DontCompileHugeMethods -XX:MaxNodeLimit=240000 -XX:NodeLimitFudgeFactor=8000 -XX:+OptimizeStringConcat -XX:+PerfDisableSharedMem -Dgale.log.warning.offline.mode=false -Dgale.log.warning.root=false -DGeyser.RakGlobalPacketLimit=100000 -DGeyser.RakPacketLimit=1500 -DGeyser.RakRateLimitingDisabled=true -Djava.awt.headless=true -Djava.net.preferIPv4Stack=true -DLeaf.disable-vanilla-profiler=true -DLeaf.enableFMA=true -Dpaper.explicit-flush=true -Dpaper.playerconnection.keepalive=180 -Dsun.net.maxDatagramSockets=16384 -Dterminal.ansi=true -Dterminal.jline=false`

> [!NOTE]
> Work in progress, will update soon.

---

## Technical Details

### Base Image
- **Distribution**: Amazon Corretto
- **Version**: 25.0.1 LTS
- **OS**: Ubuntu 22.04 LTS (Jammy)
- **Architecture**: amd64

### Included Packages
- `curl`, `wget` - Download utilities
- `git` - Version control
- `fontconfig` - Font rendering support
- `ca-certificates` - SSL/TLS support
- `tzdata` - Timezone data
- `iproute2` - Network utilities

### Security Features
- ✅ Non-root user execution (`container:container`)
- ✅ Minimal package installation
- ✅ No unnecessary ports exposed
- ✅ Regular security updates via base image

---

## Troubleshooting

<details>
<summary><b>Container won't start</b></summary>

**Symptoms**: Server fails to start, no output in console

**Solutions**:
1. Check that `SERVER_JARFILE` is accessible
2. Verify sufficient disk space
3. Review Pterodactyl console logs
4. Ensure proper file permissions

</details>

<details>
<summary><b>Out of Memory (OOM) errors</b></summary>

**Symptoms**: Server crashes with `OutOfMemoryError`

**Solutions**:
1. Increase `SERVER_MEMORY` allocation
2. Optimize JVM flags for your workload
3. Monitor actual memory usage
4. Consider upgrading server resources

</details>

<details>
<summary><b>EULA not accepted</b></summary>

**Symptoms**: Server stops with EULA message

**Solutions**:
1. Set `AUTO_EULA=true` in egg variables
2. Manually create `eula.txt` with `eula=true`
3. Restart the server

</details>

<details>
<summary><b>Java version mismatch</b></summary>

**Symptoms**: Application requires different Java version

**Solutions**:
1. Verify your application supports Java 25
2. Check Docker image version: `docker run --rm ssdarealest/corretto-xx-pterodactyl:latest java -version`
3. Use appropriate egg for your Java version

</details>

---

## Documentation

- **[Quick Start Guide](QUICKSTART.md)** - Get up and running in 5 minutes
- **[Egg Configuration](egg-amazon-corretto--universal.json)** - Pterodactyl egg specification
- **[Dockerfile](/docker/)** - Image build configuration
- **[License](LICENSE)** - MIT License

---

## Contributing

Contributions are welcome! Here's how you can help:

- **Report bugs** via GitHub Issues
- **Suggest features** for future releases
- **Improve documentation** with pull requests
- **Share configurations** for different games
- **Star this repository** if you find it useful

---

## License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## Credits

- **[Amazon Corretto](https://aws.amazon.com/corretto/)** - Java distribution
- **[Pterodactyl Panel](https://pterodactyl.io/)** - Game server management
- **[Aikar](https://aikar.co/)** - JVM optimization flags
- **[MeowIce's Optimization Flags](https://github.com/MeowIce/meowice-flags)** - Optimized JVM flags for Corretto
- **Community contributors** - Testing and feedback

---

## Star History

If this project helps you, please consider giving it a ⭐! It'll help me a lot!

---

<div align="center">

**Built with ❤️ for the gaming community**

Ready for production | High-quality & perfomance | LTS & Zero-cost updates | Secured by Amazon

This project is heavity inspired by the original repository, [Java 25 Docker for Pterodactyl by @janxhg](https://github.com/janxhg/java-25-pterodactyl). Give him a star!

[Report Bug](https://github.com/ssdarealest/amazon-corretto-pterodactyl/issues) • [Request Feature](https://github.com/ssdarealest/amazon-corretto-pterodactyl/issues) • [Join my community](https://discord.langbangvn.net) • [Contact me through Discord](https://discord.com/users/727497287777124414) • [...Teto?](https://youtu.be/UsjsYMo3O1Q) • [MCK - HVL](https://www.youtube.com/playlist?list=PLG5bpInXG8Sc)

![Alyosha's Text (large)](assets/alyosha-text--large.png)

</div>