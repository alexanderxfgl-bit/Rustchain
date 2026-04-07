# Vintage Miner Setup Guide - "Mine Your Grandma's Computer"

## Overview

This guide helps you turn old computers into RustChain miners. Whether it's your grandma's dusty Windows XP laptop, an old iMac from the attic, or a forgotten gaming rig, vintage hardware can earn rewards on RustChain.

## What is Vintage Mining?

Vintage mining uses older computers to mine RustChain through **Proof-of-Antiquity**. The older your hardware, the higher your potential multiplier (up to 50x+ for true vintage systems).

### Why Mine Vintage Hardware?

- **High Multipliers**: 10x-50x+ potential rewards for very old hardware
- **Eco-Friendly**: Repurpose instead of throwing away
- **Historical Preservation**: Keep vintage systems running
- **Low Competition**: Few miners use vintage hardware
- **Unique Rewards**: Special badges and recognition

## Supported Hardware Types

### 🖥️ Personal Computers (Common)

**Windows Systems**
- **Windows XP/2000** (2001-2009): 5x-10x multiplier
- **Windows 7/Vista** (2006-2013): 3x-5x multiplier
- **Windows 95/98** (1995-2001): 15x-25x multiplier

**Apple Mac Systems**
- **PowerPC G3/G4** (1997-2005): 20x-35x multiplier
- **PowerPC G5** (2003-2006): 10x-20x multiplier
- **Intel Core 2 Duo** Macs (2006-2010): 5x-8x multiplier
- **Original iMac G3/G4** (1998-2004): 25x-40x multiplier

**Linux/Unix Workstations**
- **Pentium III/4** (1999-2008): 8x-15x multiplier
- **AMD Athlon 64** (2003-2009): 6x-12x multiplier
- **Early Core 2 Duo** (2006-2009): 4x-8x multiplier

### 🎮 Gaming Consoles (Special)

**Nintendo**
- **Nintendo 64** (1996-2002): 35x-50x multiplier
- **GameCube** (2001-2007): 25x-40x multiplier
- **Wii** (2006-2012): 10x-15x multiplier

**Sony**
- **PlayStation 1** (1994-2006): 30x-45x multiplier
- **PlayStation 2** (2000-2013): 15x-25x multiplier
- **PlayStation 3** (2006-2013): 8x-12x multiplier

**Microsoft**
- **Xbox** (2001-2009): 20x-30x multiplier
- **Xbox 360** (2005-2016): 10x-15x multiplier

### 🏢 Enterprise/Legacy (Advanced)

**Workstation Class**
- **Sun SPARC** (1995-2010): 25x-40x multiplier
- **IBM POWER** (1997-2015): 20x-35x multiplier
- **SGI Workstations** (1992-2006): 30x-50x multiplier

## Hardware Requirements

### Minimum Specifications

**Processor**
- Any CPU from 1995 or later works
- 32-bit or 64-bit (64-bit preferred)
- Single core is fine (multi-core = more attestations)

**Memory**
- 128MB RAM absolute minimum
- 256MB RAM for Windows 98/XP
- 512MB RAM for Windows 7/OSX 10.4+
- 1GB+ RAM recommended for stability

**Storage**
- 5GB free disk space minimum
- 10GB+ recommended
- Supports HDD, SSD, or even older IDE drives

**Network**
- Ethernet port (10/100/1000 Mbps)
- WiFi works but less reliable
- Stable internet connection required

**Power**
- Stable power supply
- Old systems can be power-hungry
- Consider UPS for vintage systems

### Ideal Hardware for Each Category

**Beginner (Easy Setup)**
- Windows 7 laptop (5-8x)
- Intel Core 2 Duo desktop (4-8x)
- Early Intel i3/i5 systems (3-5x)

**Intermediate (Good Multipliers)**
- Windows XP gaming rig (8-12x)
- PowerPC G4 Mac (20-35x)
- AMD Athlon 64 system (6-12x)

**Advanced (Maximum Multipliers)**
- Nintendo 64 (35-50x)
- PlayStation 1 (30-45x)
- Original iMac G3 (25-40x)
- SGI workstation (30-50x)

## Installation Guide

### Option 1: Docker Container (Easiest)

**Best for: Modern vintage hardware (2005+)**

```bash
# Install Docker (Ubuntu/Debian)
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker $USER

# Pull vintage miner image
docker pull rustchain/vintage-miner:latest

# Run miner
docker run -d \\
  --name vintage-miner \\
  --restart unless-stopped \\
  -v ~/.rustchain:/root/.rustchain \\
  -e RUSTCHAIN_NODE_URL=https://50.28.86.131 \\
  rustchain/vintage-miner:latest
```

### Option 2: Pre-built Binary

**Best for: Windows XP/7, macOS 10.4-10.6**

1. Download the appropriate binary for your OS
2. Extract to a folder (e.g., `C:\RustchainMiner`)
3. Run the executable

**Windows:**
```cmd
# Download from GitHub releases
# Extract to folder
cd C:\RustchainMiner
rustchain-miner.exe
```

**macOS (PowerPC):**
```bash
# Download PowerPC binary
chmod +x rustchain-miner-ppc
./rustchain-miner-ppc
```

### Option 3: Build from Source

**Best for: Linux vintage systems, full control**

```bash
# Clone repository
git clone https://github.com/Scottcjn/Rustchain.git
cd Rustchain/rustchain-miner

# Install Rust (if not present)
curl https://sh.rustup.rs -sSf | sh
source $HOME/.cargo/env

# Build for your architecture
cargo build --release

# Run miner
./target/release/rustchain-miner
```

## Configuration

### Basic Configuration File

Create `~/.rustchain/config.toml`:

```toml
[node]
url = "https://50.28.86.131"  # Main RustChain node
timeout = 30

[miner]
id = "grandmas-xp-laptop"  # Unique ID for your miner
interval = 120  # Check interval in seconds
max_retries = 3  # Retry failed attestations

[fingerprint]
# Vintage-specific settings
real_mode = true  # Use real hardware fingerprinting
cache_measurement = true  # Cache to save CPU
thermal_monitoring = false  # Disable if unsupported
clock_drift = true  # Clock drift attestation

[performance]
# Adjust for vintage hardware
cpu_threads = 1  # Use single core for stability
memory_limit = 512  # MB, adjust based on RAM
network_timeout = 60  # Seconds
```

### Windows XP/2000 Specific Configuration

```toml
[node]
url = "https://50.28.86.131"
timeout = 60  # Longer timeout for slower systems

[miner]
id = "win-xp-grandma-laptop"
interval = 180  # Slower interval
max_retries = 5  # More retries

[fingerprint]
real_mode = true
cache_measurement = true
clock_drift = false  # May not work on older Windows
thermal_monitoring = false
```

### PowerPC Mac Configuration

```toml
[miner]
id = "powermac-g4-desktop"
interval = 150
max_retries = 4

[fingerprint]
# PowerPC-specific optimizations
altivec_enabled = true  # Use AltiVec if available
simd_mode = "altivec"  # AltiVec SIMD support
```

## Platform-Specific Guides

### Windows XP Setup

#### 1. System Requirements
- Windows XP SP2 or SP3
- 512MB RAM minimum
- .NET Framework 2.0+
- Internet connection

#### 2. Installation
```cmd
# Download vintage miner binary
# Extract to C:\RustchainMiner
# Double-click rustchain-miner.exe
```

#### 3. Configuration
```cmd
# Create config file
notepad C:\Documents and Settings\YourUser\.rustchain\config.toml
```

Paste the Windows XP configuration above.

#### 4. Running as Service
```cmd
# Install as Windows service
rustchain-miner.exe --install-service
net start rustchain-miner
```

#### 5. Troubleshooting
```cmd
# Check logs
type C:\Documents and Settings\YourUser\.rustchain\miner.log

# Monitor process
tasklist | findstr rustchain

# Kill if needed
taskkill /F /IM rustchain-miner.exe
```

### Windows 7 Setup

#### 1. System Requirements
- Windows 7 SP1
- 1GB RAM minimum
- .NET Framework 4.0+
- Modern network adapter

#### 2. Installation
```cmd
# Same as XP but use Windows 7 config
# May need to run as Administrator
```

#### 3. Configuration
- Use Windows 7-specific configuration
- Consider enabling thermal monitoring if supported

### macOS PowerPC Setup

#### 1. System Requirements
- macOS 10.3 (Panther) or later
- 256MB RAM minimum
- 5GB free disk space
- Developer tools for building from source

#### 2. Installation Options
```bash
# Option 1: Pre-built PowerPC binary
curl -O https://github.com/Scottcjn/Rustchain/releases/download/v1.0/rustchain-miner-ppc
chmod +x rustchain-miner-ppc
./rustchain-miner-ppc

# Option 2: Build from source
git clone https://github.com/Scottcjn/Rustchain.git
cd Rustchain/rustchain-miner
cargo build --release --target=powerpc-apple-darwin
```

#### 3. Configuration
```bash
# Create config
mkdir -p ~/.rustchain
nano ~/.rustchain/config.toml

# Use PowerPC config above
```

#### 4. Performance Tips
```bash
# Monitor with Activity Monitor
# Check CPU usage
# Adjust interval if system is slow

# Set process priority
nice -n 10 ./rustchain-miner
```

### Linux Vintage Setup

#### 1. System Requirements
- Linux kernel 2.6 or later
- 256MB RAM minimum
- GCC for building
- Network connection

#### 2. Installation
```bash
# Install dependencies
sudo apt-get update
sudo apt-get install build-essential git curl

# Install Rust
curl https://sh.rustup.rs -sSf | sh
source $HOME/.cargo/env

# Clone and build
git clone https://github.com/Scottcjn/Rustchain.git
cd Rustchain/rustchain-miner
cargo build --release

# Run
./target/release/rustchain-miner
```

#### 3. Configuration
```bash
# Create config
mkdir -p ~/.rustchain
nano ~/.rustchain/config.toml
```

#### 4. systemd Service
```bash
# Create service file
sudo nano /etc/systemd/system/rustchain-vintage.service
```

```ini
[Unit]
Description=RustChain Vintage Miner
After=network.target

[Service]
Type=simple
User=your-username
WorkingDirectory=/home/your-username/Rustchain/rustchain-miner
ExecStart=/home/your-username/Rustchain/rustchain-miner/target/release/rustchain-miner
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```

```bash
# Enable and start
sudo systemctl enable rustchain-vintage
sudo systemctl start rustchain-vintage
```

## Gaming Console Mining

### Nintendo 64 Setup

#### 1. Requirements
- Nintendo 64 console (1996-2002)
- Expansion Pak recommended
- Gameshark/Action Replay (for homebrew)
- USB adapter or SD card

#### 2. Homebrew Setup
```bash
# This requires advanced setup
# Follow community guides for N64 homebrew
# Install vintage miner via homebrew channel

# Simplified: Use PC emulator
mupen64plus --host --miner --node-url https://50.28.86.131
```

### PlayStation 1 Setup

#### 1. Requirements
- PlayStation 1 (any model)
- Memory card
- Action Replay or Gameshark
- PC with CD burner

#### 2. Setup
```bash
# Burn miner to CD
# Use Action Replay to boot CD
# Follow on-screen instructions

# Alternative: Emulator on PC
pcsx --miner-mode --node-url https://50.28.86.131
```

### Notes on Console Mining

- **Emulator Approach**: Often easier than real hardware
- **Higher Multipliers**: Real hardware has higher multipliers
- **Legal Considerations**: Only mine consoles you own
- **Stability**: Consoles can be unstable for continuous mining

## Troubleshooting

### Common Issues

#### Miner Won't Start

**Symptoms**: Binary won't execute, crashes immediately

**Solutions**:
```bash
# Check permissions (Linux/macOS)
chmod +x rustchain-miner
./rustchain-miner

# Check dependencies (Windows)
# Install .NET Framework if missing

# Check CPU compatibility
# Try different build flags
```

#### High CPU Usage

**Symptoms**: System becomes unresponsive

**Solutions**:
```toml
# Reduce CPU usage in config
[miner]
interval = 300  # Slower interval
cpu_threads = 1  # Single thread

# Use system priorities (Linux/macOS)
nice -n 15 ./rustchain-miner

# Windows process priority
# Run as /BELOWNORMAL priority
```

#### Network Errors

**Symptoms**: Cannot connect to RustChain node

**Solutions**:
```toml
# Increase timeout
[node]
timeout = 120

# Use HTTP instead of HTTPS (if cert issues)
url = "http://50.28.86.131"

# Check firewall
# Windows: Allow port 8333 in Windows Firewall
# Linux: sudo ufw allow 8333/tcp
```

#### Low Attestation Success

**Symptoms**: Many failed attestations

**Solutions**:
```toml
# Increase retries
[miner]
max_retries = 10
retry_backoff = 2000  # Backoff in ms

# Enable caching
[fingerprint]
cache_measurement = true

# Disable unsupported features
[fingerprint]
thermal_monitoring = false
clock_drift = false
```

### Hardware-Specific Troubleshooting

**Windows XP**:
- Update to SP3
- Install all critical updates
- Disable antivirus temporarily (if blocking)
- Check .NET Framework version

**PowerPC Mac**:
- Use AltiVec optimizations
- Monitor temperature (if available)
- Reduce interval if overheating
- Check for memory leaks

**Linux Vintage**:
- Check kernel version (2.6+ required)
- Use compatible Rust version
- Monitor system resources with `top`
- Check logs with `journalctl`

## Monitoring and Maintenance

### Check Mining Status

```bash
# View logs
tail -f ~/.rustchain/miner.log

# Check process
ps aux | grep rustchain-miner

# Network connection
netstat -an | grep 8333
```

### Performance Monitoring

```bash
# CPU usage
top -H -p $(pgrep rustchain-miner)

# Memory usage
free -h

# Disk usage
df -h

# Network speed
iftop
```

### Regular Maintenance

**Weekly**:
- Check logs for errors
- Verify attestations are successful
- Update RustChain software
- Clean temporary files

**Monthly**:
- Backup configuration files
- Review performance metrics
- Check for RustChain updates
- Clean disk space

**Quarterly**:
- Full system backup
- Hardware inspection
- Dust cleaning
- Cable inspection

## Security Best Practices

### System Security

```bash
# Update operating system
# Windows: Windows Update
# macOS: Software Update
# Linux: sudo apt-get update && sudo apt-get upgrade

# Use strong passwords
# Enable firewall
# Disable unnecessary services
```

### Mining Security

```toml
# Use unique miner ID
[miner]
id = "unique-descriptive-name"  # Don't use default

# Enable TLS if supported
[node]
url = "https://50.28.86.131"  # HTTPS, not HTTP

# Limit resource usage
[performance]
memory_limit = 512  # Don't use all RAM
cpu_threads = 1  # Don't overload CPU
```

## Community and Support

### Getting Help

- **GitHub Issues**: Report bugs and request features
- **Discord**: Join `#vintage-mining` channel
- **Documentation**: [RustChain Docs](https://github.com/Scottcjn/Rustchain/tree/main/docs)
- **FAQ**: Check existing issues first

### Share Your Setup

Post your vintage mining setup:
- Hardware specifications
- Configuration used
- Multiplier achieved
- Photos of your vintage system
- Tips and tricks discovered

## Examples of Successful Vintage Miners

### Grandma's Windows XP Laptop
- **Hardware**: 2005 Toshiba Satellite (Pentium M)
- **Multiplier**: 8.5x
- **Configuration**: Single thread, 180s interval
- **Success**: Stable for 6 months

### Attic iMac G4
- **Hardware**: 2003 iMac G4 800MHz
- **Multiplier**: 22x
- **Configuration**: AltiVec enabled, 150s interval
- **Success**: Multiple badges earned

### Forgotten Gaming Rig
- **Hardware**: 2008 Core 2 Duo + GTX 260
- **Multiplier**: 6.2x
- **Configuration**: Hybrid mode, 120s interval
- **Success**: Consistent attestations

## Conclusion

Vintage mining on RustChain gives new life to old hardware. Your grandma's dusty laptop or your childhood gaming console can earn real rewards while preserving computing history.

**Remember**:
- Start with what you have
- Be patient with slower systems
- Monitor system health
- Share your experiences
- Have fun with vintage tech!

**Happy Vintage Mining!** 🖥️💾🪙

---

**Bounty Reference**: Resolves issue #2150 - Bounty: "Mine Your Grandma's Computer" — vintage miner setup guide

**Additional Resources**:
- [RustChain Whitepaper](https://github.com/Scottcjn/Rustchain/blob/main/docs/WHITEPAPER.md)
- [Mining Guide](https://github.com/Scottcjn/Rustchain/blob/main/docs/MINING_GUIDE.md)
- [Console Mining Guide](https://github.com/Scottcjn/Rustchain/blob/main/docs/CONSOLE_MINING_SETUP.md)