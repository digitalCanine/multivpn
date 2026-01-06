# digitalCanine's MultiVPN

A flexible VPN manager script that supports multiple VPN providers through OpenVPN configuration files. Features an interactive rofi menu system for easy provider, country, city, and server selection.

## ✨ Features

- 🌍 **Multi-Provider Support** - Manage multiple VPN providers from one interface
- 📍 **Hierarchical Selection** - Choose provider → country → city → server
- 🎲 **Random Selection** - Randomly select provider, country, city, or server
- 🔒 **Scrambled Connection Support** - Automatically detects and offers scrambled servers when available
- 🔐 **Per-Provider Authentication** - Each provider has its own credentials file
- 📊 **Connection Feedback** - Desktop notifications with connection status and public IP
- ⚡ **Smart Server Detection** - Automatically parses OpenVPN files and builds dynamic menus
- 🗺️ **Global Coverage** - Supports 70+ country codes across all continents

## 📋 Requirements

- `bash`
- `openvpn`
- `rofi`
- `notify-send` (libnotify)
- `curl`
- `sudo` privileges

## 🚀 Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/digitalcanine/multivpn
   cd multivpn
   ```

2. Create the providers directory structure:
   ```bash
   mkdir -p providers
   ```

3. Make the script executable:
   ```bash
   chmod +x dc-multivpn.sh
   ```

## 📁 Directory Structure

```
multivpn/
├── dc-multivpn.sh          # Main script
└── providers/              # Providers directory
    ├── provider1/          # Provider name (e.g., nordvpn, mullvad, pia)
    │   ├── auth           # Authentication file
    │   └── servers/       # OpenVPN config files
    │       ├── city1-us-001.ovpn
    │       ├── city1-us-002.ovpn
    │       ├── city2-uk-001-scramble.ovpn
    │       └── ...
    └── provider2/
        ├── auth
        └── servers/
            └── ...
```

## ⚙️ Setup

### 1. Add a VPN Provider

For each VPN provider you want to use:

```bash
cd providers
mkdir your-provider-name
cd your-provider-name
```

### 2. Create Authentication File

Create an `auth` file with your credentials:

```bash
cat > auth << EOF
your_username
your_password
EOF
```

**Security note:** Keep your auth file secure:
```bash
chmod 600 auth
```

### 3. Add OpenVPN Configuration Files

Create a `servers` directory and add your `.ovpn` files:

```bash
mkdir servers
# Copy your .ovpn files here
cp /path/to/configs/*.ovpn servers/
```

### 4. OpenVPN File Naming Convention

The script expects OpenVPN files to follow this naming format:

```
city-countrycode-###.ovpn
city-countrycode-###-scramble.ovpn
```

**Examples:**
- `new-york-us-001.ovpn`
- `london-uk-042.ovpn`
- `tokyo-jp-015-scramble.ovpn`
- `los-angeles-us-100.ovpn`

**Format breakdown:**
- `city`: City name (lowercase, hyphens for spaces)
- `countrycode`: Two-letter country code (lowercase)
- `###`: Three-digit server number
- `-scramble` (optional): Indicates obfuscated/scrambled server

### Supported Country Codes

The script recognizes 70+ country codes including:

**North America:** us, ca, mx  
**Europe:** uk/gb, de, fr, nl, ch, es, it, se, no, dk, fi, pl, cz, and more  
**Asia:** jp, kr, sg, hk, tw, in, th, my, id, ph, vn  
**Oceania:** au, nz  
**South America:** br, ar, cl, co, pe  
**Middle East:** ae, sa, il, qa  
**Africa:** za, eg, ng, ke, ma

## 🎮 Usage

### Run the script:

```bash
./dc-multivpn.sh
```

Or bind it to a keyboard shortcut (example for sxhkd):

```bash
alt + shift + v
    /path/to/multivpn/dc-multivpn.sh
```

### Interactive Menu Flow:

1. **Select Provider** - Choose from your configured providers or select random
2. **Select Country** - Choose a country or random
3. **Select City** - Choose a city or random
4. **Select Connection Type** - Regular or Scrambled (if both available)
5. **Select Server** - Choose specific server or random
6. **Enter Password** - Provide sudo password for OpenVPN
7. **Connection Status** - Notification shows connection details and public IP

### Menu Options:

- **[Random Provider]** - Selects a random provider
- **[Random Country]** - Selects a random country from the provider
- **[Random City]** - Selects a random city
- **[Random Server]** - Selects a random server
- **[Disconnect]** - Kills any active OpenVPN connection

## 🔧 Configuration

### Customizing Rofi Appearance

Edit the `ROFI` variable in the script:

```bash
ROFI="rofi -dmenu -i -theme your-theme"
```

### Changing Notification Behavior

Modify the `NOTIFY` variable:

```bash
NOTIFY="notify-send -t 5000"  # Show notifications for 5 seconds
```

### Adjusting Connection Timeout

Edit the sleep duration after OpenVPN launch (line ~390):

```bash
sleep 8  # Wait 8 seconds for connection to establish
```

## 🛡️ Security Considerations

- **Auth Files:** Keep authentication files secure with `chmod 600 auth`
- **Sudo Access:** The script requires sudo privileges to run OpenVPN
- **Password Storage:** Consider using `sudo` with NOPASSWD for OpenVPN in `/etc/sudoers` to avoid entering password each time:
  ```
  your_username ALL=(ALL) NOPASSWD: /usr/bin/openvpn, /usr/bin/pkill openvpn
  ```

## 🐛 Troubleshooting

### No providers found
- Ensure you have created provider directories in the `providers/` folder
- Check that each provider has an `auth` file and `servers/` directory

### No servers found
- Verify your `.ovpn` files follow the naming convention: `city-cc-###.ovpn`
- Ensure files are in the `providers/PROVIDER_NAME/servers/` directory

### Connection fails
- Check that your `auth` file contains correct credentials
- Verify OpenVPN configs are valid
- Check system logs: `journalctl -u openvpn --since "5 minutes ago"`

### IP not showing
- The script waits 8 seconds and retries 3 times
- Check your internet connection
- Verify `curl` is installed

## 📝 Example Setup

Complete example for NordVPN:

```bash
cd multivpn/providers
mkdir nordvpn
cd nordvpn

# Create auth file
cat > auth << EOF
myemail@example.com
mypassword123
EOF
chmod 600 auth

# Create servers directory
mkdir servers

# Download OpenVPN configs from NordVPN and rename them
# e.g., us9999.nordvpn.com.tcp.ovpn → new-york-us-001.ovpn
cp ~/Downloads/us9999.nordvpn.com.tcp.ovpn servers/new-york-us-001.ovpn
cp ~/Downloads/uk2345.nordvpn.com.tcp.ovpn servers/london-uk-001.ovpn
```

## 🤝 Contributing

Contributions are welcome! Feel free to submit issues or pull requests for:
- Additional country code support
- Bug fixes
- Feature enhancements
- Documentation improvements

## 📄 License

This project is open source and available under the MIT License.

## 🔗 Related Projects

- [bspwm-rice](https://github.com/digitalcanine/bspwm-rice) - My complete bspwm desktop configuration that includes MultiVPN integration

---

