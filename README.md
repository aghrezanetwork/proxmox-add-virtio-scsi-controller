# proxmox-add-virtio-scsi-controller

**How to add a VirtIO SCSI controller alongside an existing VMware PVSCSI controller in Proxmox VE (Windows 11 guest) — a tested, step-by-step guide in English and Persian.**

**راهنمای گام‌به‌گام و آزمایش‌شده برای افزودن کنترلر VirtIO SCSI در کنار کنترلر VMware PVSCSI در Proxmox VE (ویندوز ۱۱) — به دو زبان فارسی و انگلیسی.**

---

## 🌐 Read the guide online / مطالعه راهنما

The guide is also available as a browsable web page via GitHub Pages:

- 🇬🇧 **English:** [proxmox-virtio-scsi-pvscsi-en.html](https://aghrezanetwork.github.io/proxmox-add-virtio-scsi-controller/proxmox-virtio-scsi-pvscsi-en.html)
- 🇮🇷 **فارسی:** [proxmox-virtio-scsi-pvscsi-fa.html](https://aghrezanetwork.github.io/proxmox-add-virtio-scsi-controller/proxmox-virtio-scsi-pvscsi-fa.html)
- 🗂️ Landing page / صفحه اصلی: [index.html](https://aghrezanetwork.github.io/proxmox-add-virtio-scsi-controller/)

## 📁 Files / فایل‌ها

| File | Language |
|---|---|
| [`proxmox-virtio-scsi-pvscsi-en.html`](proxmox-virtio-scsi-pvscsi-en.html) | English |
| [`proxmox-virtio-scsi-pvscsi-fa.html`](proxmox-virtio-scsi-pvscsi-fa.html) | فارسی (Persian) |
| [`index.html`](index.html) | Bilingual landing page |

## 📝 What this guide covers / محتوای راهنما

- Keeping the existing `scsihw: pvscsi` controller and its disks untouched / حفظ کنترلر PVSCSI و دیسک‌های موجود
- Backing up `/etc/pve/qemu-server/<VMID>.conf` / پشتیبان‌گیری از فایل تنظیمات
- Adding the second controller: `qm set <VMID> --args '-device virtio-scsi-pci,id=virtioscsi1,bus=pci.0'` / افزودن کنترلر دوم
- Verifying in Windows 11 Device Manager (Storage controllers) and installing the VirtIO driver from the ISO / تأیید در Device Manager و نصب درایور VirtIO
- Troubleshooting, rollback (`qm set <VMID> --delete args`) and a final checklist / عیب‌یابی، بازگشت به وضعیت قبلی و چک‌لیست نهایی

## ⚠️ Disclaimer / هشدار

Tested on Proxmox VE 9.2 with a Windows 11 guest. Always try it on a test VM first, and keep a backup of your VM configuration. A custom `args` controller is not managed by the Proxmox UI like regular hardware — verify migration and backup/restore behavior in your own environment.

آزمایش‌شده روی Proxmox VE 9.2 با ویندوز ۱۱. ابتدا روی ماشین آزمایشی امتحان کنید و از تنظیمات VM نسخه پشتیبان بگیرید. کنترلر تعریف‌شده با `args` مانند سخت‌افزار معمولی در رابط Proxmox مدیریت نمی‌شود — رفتار Migration و Backup/Restore را در محیط خودتان بررسی کنید.
