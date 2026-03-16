# webmin-nftables-editor

A Webmin module for editing, testing and applying nftables firewall rules directly from the Webmin interface.

## Features

- Syntax highlighted editor for `/etc/nftables.conf`
- Save, Test, Apply and List buttons
- Test runs against a temporary file — never touches the real config
- Automatic backup to `/etc/nftables.conf.bak` on Save and Apply
- Automatic fail2ban restart after Apply (if fail2ban is active)
- Works with Authentic Theme 26.x

## Requirements

- Webmin 2.x
- Authentic Theme 26.x
- nftables (`/usr/sbin/nft`)
- systemd (`/usr/bin/systemctl`)
- Perl (no extra modules required)

## Installation

### Download the module
```bash
wget https://github.com/YOURUSER/webmin-nftables-editor/releases/download/v1.0/nftables-editor.wbm.gz
```

### Install via Webmin UI

1. Go to **Webmin → Webmin Configuration → Webmin Modules**
2. Click **Install Module**
3. Select **From uploaded file**
4. Upload `nftables-editor.wbm.gz`
5. Click **Install Module**

### Install via command line
```bash
perl /usr/share/webmin/install-module.pl nftables-editor.wbm.gz
```

### Download CodeMirror (required)
```bash
wget -O /usr/share/webmin/nftables-editor/codemirror.min.js \
  https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/codemirror.min.js

wget -O /usr/share/webmin/nftables-editor/codemirror.min.css \
  https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/codemirror.min.css

wget -O /usr/share/webmin/nftables-editor/simple.js \
  https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.65.16/addon/mode/simple.js
```

## Usage

The module appears under **Networking** in the Webmin menu.

| Button | Description |
|--------|-------------|
| **Save** | Saves the editor content to `/etc/nftables.conf` |
| **Test** | Checks syntax without touching the real config |
| **Apply** | Saves and loads the rules into the kernel, restarts fail2ban if active |
| **List** | Shows the currently active ruleset loaded in the kernel |

## Syntax highlighting

| Color | Meaning |
|-------|---------|
| Blue bold | `table`, `chain`, `set` |
| Green bold | `accept` |
| Red bold | `drop`, `reject` |
| Purple | Port numbers |
| Yellow | Quoted strings (interface names) |
| White italic | Chain types (`input`, `output`, `forward`) |
| Grey italic | Comments |

## fail2ban

If fail2ban is configured to use nftables (`banaction = nftables-multiport` or similar), the module automatically restarts fail2ban after Apply so its chains are re-injected into the ruleset.

## License

MIT
