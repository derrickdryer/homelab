# Storage Architecture

The homelab uses centralized storage powered by TrueNAS and ZFS.  
Storage is designed around reliability, separation of workloads, and simple management rather than excessive complexity.

Primary goals:

- Reliable data storage with ZFS redundancy
- Clear dataset separation by function
- Fast local access for services and compute nodes
- Practical backup strategy within real-world bandwidth limits

## Primary Storage Platform

- **Platform:** UGREEN DXP6800 Pro
- **Operating System:** TrueNAS
- **Filesystem:** ZFS

The storage server acts as the central data platform for:

- Application storage
- Media libraries
- Network shares
- Backup targets
- NFS/iSCSI workloads

## Pool Layout

The main pool is structured for balanced performance and redundancy.

### Data VDEVs

- 2 × RAIDZ1 vdevs
- 6 × 8 TB Seagate IronWolf Pro drives total

This layout provides:

- Disk failure protection
- Parallel performance across vdevs
- Good capacity efficiency

### Cache

- NVMe SSD cache devices for accelerated reads

### Log (SLOG)

- Mirrored NVMe devices
- Improves synchronous write performance for network storage

## Dataset Structure

Datasets are organized by purpose to simplify management and access control.

```text
mothervault/
├── apps/
├── backups/
├── iscsi/
├── media/
├── nfs/
└── shares/
```

### apps

Storage for TrueNAS-hosted applications and container data.

Typical usage:

- TrueNAS application datasets
- Jellyfin-related services
- Media management tools and supporting containers
- Persistent application storage

This dataset primarily supports media-focused services, including Jellyfin and related applications that interact with the media library.

### backups

Dedicated dataset for system and service backups.

Used for:

- Proxmox backups
- Configuration exports
- Snapshot replication targets

### iscsi

Block storage provided to external systems via iSCSI.

Used for:

- Virtual machine storage
- Specialized workloads requiring block devices

### media

Bulk storage for large media files.

Design considerations:

- High capacity over extreme performance
- Not all data requires offsite backup

### nfs

NFS exports used by Linux hosts and cluster workloads.

Common uses:

- Shared storage for compute nodes
- Kubernetes or container storage
- Service data mounts

### shares

SMB-based file shares for user access.

Typical usage:

- General file storage
- Cross-platform file access
- Personal and administrative data

## Backup Strategy

Storage follows a practical interpretation of the 3-2-1 rule.

### Local Protection

- ZFS snapshots provide rapid rollback capability
- RAIDZ redundancy protects against disk failure

## Planned Backup Strategy (Work in Progress)

A full 3-2-1 backup model is a long-term goal but is not fully implemented yet due to bandwidth and hardware limitations.

### Secondary Local Backup (Planned)

Future plans include replicating selected datasets to a secondary local storage target.

Intended focus:

- Critical system backups
- Configuration data
- Important personal files

Bulk media storage is not currently planned for full duplication.

### Offsite Backup (Planned)

Offsite backup is currently limited by upload speed and cost.

Long-term goals:

- Offsite replication of high-value datasets only
- Excluding large media datasets to reduce bandwidth usage

## Design Philosophy

This storage system favors simplicity and reliability:

- Dataset separation prevents cross-contamination of workloads
- Performance is enhanced through NVMe cache and mirrored log devices
- Backup strategy prioritizes important data over total duplication

The goal is sustainable, long-term storage rather than excessive complexity.
