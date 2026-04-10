# branch-network-vlan-design
VLAN-based branch network design using Cisco Packet Tracer with inter-VLAN routing, DHCP, and wireless connectivity.

##  VLAN & IP Addressing Scheme

| Department | VLAN ID | Network (Subnet) | Gateway | DHCP Range |
|------------|---------|------------------|---------|-------------|
| Admin/IT | 10 | 192.168.1.0/26 | 192.168.1.1 | 192.168.1.2 – 192.168.1.62 |
| Finance/HR | 20 | 192.168.1.64/26 | 192.168.1.65 | 192.168.1.66 – 192.168.1.126 |
| Customer Service/Reception | 30 | 192.168.1.128/26 | 192.168.1.129 | 192.168.1.130 – 192.168.1.190 |

- Subnet mask: **255.255.255.192** (/26)
- Total usable hosts per subnet: **62**
- No overlap between VLAN subnets

---

## ⚙️ Device Configuration Highlights

### Router (Cisco 2901)
- **Interface G0/0**: Connect to ISP (192.168.1.0 network)
- **Interface G0/1.10**, **G0/1.20**, **G0/1.30**: Subinterfaces for VLAN routing
- **DHCP Pools**: Separate pools for each VLAN
- **Inter-VLAN Routing**: Enabled via subinterfaces

### Switch (Cisco 2960)
- **Port to router**: Trunk (802.1Q)
- **Access ports**: Assigned to respective VLANs for wired devices
- **AP ports**: Access mode in respective VLAN

### Wireless Access Points
- **SSID per department**:
  - `Admin-WiFi` (VLAN 10)
  - `Finance-WiFi` (VLAN 20)
  - `Customer-WiFi` (VLAN 30)
- Security: WPA2-PSK

---

## 📂 Repository Contents

| File | Description |
|------|-------------|
| `image.png` | Project requirements statement |
| `Small Office.png` | Network topology diagram |
| `configs/router_config.txt` | Cisco router configuration |
| `configs/switch_config.txt` | Cisco switch configuration |
| `README.md` | Project documentation |

---

## 🚀 How to Simulate/Test

1. Use **Cisco Packet Tracer** or **GNS3**
2. Load the provided configuration files
3. Verify:
   - Hosts receive IPs via DHCP
   - Pings between devices in different VLANs succeed
   - Wireless clients associate with correct SSID and get correct VLAN IP

---

## 🧪 Sample Verification Commands

```bash
# On router
show ip dhcp binding
show ip route
show vlan

# On switch
show vlan brief
show interfaces trunk

# On PC
ipconfig /all
ping 192.168.1.65   # Ping Finance/HR gateway from Admin PC
