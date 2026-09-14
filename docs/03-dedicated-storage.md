# Dedicated Enterprise Storage

## Objective

Separate the operating system from company business data on `storage-01`.

The original architecture stored Ubuntu Server and company data on the same virtual disk.

The new architecture uses a dedicated virtual disk for enterprise data.

---

## Final Architecture

```text
storage-01

/dev/sda — 40 GB
└── Ubuntu Server
    ├── Operating system
    ├── Packages
    ├── Logs
    └── Samba service

/dev/sdb — 60 GB
└── /dev/sdb1
    └── ext4
        └── /srv/company
            ├── engineering
            ├── finance
            ├── hr
            ├── management
            └── shared
```

## Data Volume

Device:

```text
/dev/sdb
```

Partition:

```text
/dev/sdb1
```

Partition table:

```text
GPT
```

Filesystem:

```text
ext4
```

Filesystem label:

```text
company-data
```

Permanent mount point:

```text
/srv/company
```

---

## Persistent Mount

The filesystem is mounted using its UUID through `/etc/fstab`.

```text
UUID=<company-data-uuid> /srv/company ext4 defaults,nodev,nosuid,noexec 0 2
```

Using the filesystem UUID avoids relying on device names such as `/dev/sdb1`, which may change between environments.

---

## Storage Hardening

The company-data volume uses the following mount options:

```text
nodev
nosuid
noexec
```

### nodev

Prevents device special files from being interpreted on the business-data filesystem.

### nosuid

Prevents setuid/setgid executable privileges from being honored.

### noexec

Prevents programs from being executed directly from the business-data filesystem.

---

## Migration

The new filesystem was initially mounted at:

```text
/mnt/company-data
```

Existing data from:

```text
/srv/company
```

was migrated using:

```bash
rsync -aHAX --numeric-ids
```

This preserved:

- users and groups
- permissions
- timestamps
- ACLs
- extended attributes
- hard links

Before the final cutover, Samba was stopped and a final synchronization was performed.

---

## Validation

The new filesystem was verified using:

```bash
findmnt /srv/company
df -hT /srv/company
```

Expected result:

```text
/srv/company → /dev/sdb1
Filesystem   → ext4
Capacity     → ~59 GB
```

Department ownership and permissions were also verified.

Example:

```text
finance → root:finance
hr → root:hr
engineering → root:engineering
management → root:management
shared → root:company-shared
```

---

## Reboot Persistence Test

`storage-01` was fully rebooted after the migration.

After reboot:

- `/dev/sdb1` mounted automatically
- `/srv/company` contained the migrated data
- Samba started automatically
- department permissions survived
- Samba users retained access
- Sarah retained access to Finance
- existing SMB files remained available

Result:

```text
PASS
```

---

## Rollback Strategy

The original dataset remains temporarily available at:

```text
/srv/company-old
```

A dry-run comparison was performed:

```bash
rsync -aHAXcn --numeric-ids --delete --itemize-changes \
/srv/company-old/ /srv/company/
```

No differences were reported.

Therefore the rollback dataset currently matches the production data volume.

The rollback copy will remain in place until the backup and restore system has been implemented and validated.

---

## Result

The storage server now separates:

```text
Operating system → system disk
Business data    → dedicated data disk
```

This improves:

- isolation
- maintainability
- recoverability
- security
- capacity management
- backup design
- future monitoring