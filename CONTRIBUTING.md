
---

## 🛠️ 2. `build.sh` (ISO Build Script)

Yeh script Kali live-build use karti hai aur dono editions ke liye config apply karti hai. (Yeh ek simplified version hai – pehli baar run karne mein time lagega.)

```bash
#!/bin/bash
set -e

echo "==> CortexSec OS ISO Builder =="
echo "==> Installing dependencies (if missing)..."
sudo apt update
sudo apt install -y live-build cdebootstrap curl git

WORK_DIR=build
mkdir -p $WORK_DIR
cd $WORK_DIR

# Clean any previous build
lb clean --purge

# Base config
lb config \
    --distribution kali-rolling \
    --archive-areas "main non-free contrib" \
    --binary-images iso-hybrid \
    --bootappend-live "boot=live components quiet splash" \
    --debian-installer live \
    --debian-installer-gui true

# Copy our custom config overrides
cp -r ../config/* config/
cp -r ../ai-integration config/includes.chroot/opt/cotx/ 2>/dev/null || true
mkdir -p config/includes.chroot/opt/cotx/optional/
cp ../config/includes.chroot/opt/cotx/optional/install-onedrive.sh config/includes.chroot/opt/cotx/optional/ 2>/dev/null || true
cp ../config/includes.chroot/opt/cotx/firstboot.sh config/includes.chroot/opt/cotx/ 2>/dev/null || true

# Build the ISO
echo "==> Building ISO (this will take a while)..."
lb build

# Move ISO to project root
ISO_FILE=$(ls -t *.iso | head -1)
mv $ISO_FILE ../cortexsec-os-$(date +%Y%m%d).iso
cd ..
echo "==> Done! ISO: cortexsec-os-*.iso"