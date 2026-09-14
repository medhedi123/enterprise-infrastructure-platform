# Changelog

## Phase 2 - Dedicated Storage

### Added

- Dedicated 60 GB enterprise data volume
- GPT partition table
- ext4 filesystem
- `company-data` filesystem label
- UUID-based persistent mounting
- Dedicated `/srv/company` mount
- `nodev`, `nosuid`, and `noexec` storage hardening
- rsync metadata-preserving migration
- Migration dry-run validation
- Samba cutover validation
- Reboot persistence testing
- Verified rollback dataset

---

## Phase 1 - Infrastructure Foundation

### Added

- Ubuntu Server `infra-gateway`
- Ubuntu Server `storage-01`
- Private `corp-net` network
- Static internal addressing
- SSH remote administration
- Samba file server
- Department groups
- Department filesystem permissions
- Samba authentication
- Department shares
- SMB access-control testing
- Successful SMB file transfer