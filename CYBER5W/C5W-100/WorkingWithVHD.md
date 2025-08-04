# 🖴 Working with Virtual Hard Disks (VHD)

---

## 📀 Physical Hard Drive

- **Physical Partition**  
  A chunk of a physical disk which may or may not contain a file system. It includes both **partitions** and **free/unallocated space**.

- **Logical Drive**  
  The user-facing part of the disk. It has:
  - A **drive letter** (e.g., C:\)
  - A **file system** (NTFS, FAT32, exFAT, etc.)
  - A defined **storage size**

---

## 💾 Virtual Hard Disk (VHD)

- A file that emulates a physical hard drive.
- Used by virtual machines and some forensic tools.

### 🗂️ Common File Formats

| Format   | Description |
|----------|-------------|
| `.vhd`   | Virtual Hard Disk – legacy format, limited to 2 TB, supported by older systems like Hyper-V (pre-Win 8) |
| `.vhdx`  | Enhanced version of VHD – supports up to 64 TB, better resiliency and performance, default for modern Hyper-V |
| `.vmdk`  | VMware Virtual Disk – used by VMware products (Workstation, Fusion, ESXi) |
| `.vdi`   | VirtualBox Disk Image – used by Oracle VirtualBox |
| `.img`   | Raw disk image format – a bit-for-bit copy of a physical drive (can be mounted like a virtual disk) |
| `.qcow2` | QEMU Copy-On-Write – used by QEMU/KVM hypervisors, supports snapshots and compression |
|`.avhd/.avhdx`| Automatic Virtual Hard Disk (differencing disks) |
---

