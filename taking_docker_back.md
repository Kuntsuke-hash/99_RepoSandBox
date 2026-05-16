# Complete Docker Backup & Restore Cheat Sheet

```text
================================================================================
                           [ PHASE 1: THE BACKUP ]
================================================================================

  1. STOP SERVICES   ──► Run:  sudo systemctl stop docker.socket
                               sudo systemctl stop docker
                                    │
                                    ▼
  2. CHOOSE BACKUP   ──► Option A (Total / Recommended):
                         Run:  sudo tar -czvf docker-total-backup.tar.gz /var/lib/docker
                                    │
                                    └─► Option B (Volumes Only):
                         Run:  sudo tar -czvf docker-volumes-backup.tar.gz /var/lib/docker/volumes
                                    │
                                    ▼
  3. SAVE CONFIGS    ──► Run:  mkdir -p ~/docker-backup
                               sudo cp /etc/docker/daemon.json ~/docker-backup/
                               cp -r ~/my-docker-projects ~/docker-backup/
                                    │
                                    ▼
  4. VERIFY FILE     ──► Run:  ls -lh docker-total-backup.tar.gz

================================================================================
                    ⚠️  SAFE TO UNINSTALL / REINSTALL DOCKER ⚠️
================================================================================

================================================================================
                          [ PHASE 2: THE RESTORE ]
================================================================================

  5. STOP NEW DOCKER ──► Run:  sudo systemctl stop docker.socket
                               sudo systemctl stop docker
                                    │
                                    ▼
  6. EXTRACT DATA    ──► If Option A (Total Restore):
                         Run:  sudo rm -rf /var/lib/docker
                               sudo tar -xzvf docker-total-backup.tar.gz -C /
                                    │
                                    └─► If Option B (Volumes Only):
                         Run:  sudo tar -xzvf docker-volumes-backup.tar.gz -C /
                                    │
                                    ▼
  7. RESTORE CONFIGS ──► Run:  sudo cp ~/docker-backup/daemon.json /etc/docker/
                                    │
                                    ▼
  8. START SERVICES  ──► Run:  sudo systemctl start docker
                                    │
                                    ▼
  9. VERIFY WORKING  ──► Run:  docker volume ls
                               cd ~/my-docker-projects && docker compose up -d
```
