# 🌐 Cisco VLAN Troubleshooting Lab

![Cisco](https://img.shields.io/badge/Cisco-Packet%20Tracer-1BA0D7?style=for-the-badge)
![Networking](https://img.shields.io/badge/Networking-VLANs-2ea44f?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Resolved-success?style=for-the-badge)

A hands-on Cisco Packet Tracer lab focused on **VLANs, inter-VLAN routing, 802.1Q trunking, and network troubleshooting**.

## 🗺️ Network Topology

```mermaid
graph TD
    R1["🌐 R1<br/>Router-on-a-Stick"]
    SW1["🔀 SW1<br/>Distribution"]
    SW2["🔀 SW2<br/>Access"]
    SW3["🔀 SW3<br/>Access"]

    PC1["💻 PC1<br/>192.168.10.11"]
    PC2["💻 PC2<br/>192.168.10.12"]
    PC3["💻 PC3<br/>192.168.20.11"]
    PC4["💻 PC4<br/>192.168.20.12"]

    R1 --> SW1
    SW1 --> SW2
    SW1 --> SW3

    SW2 --> PC1
    SW2 --> PC2
    SW3 --> PC3
    SW3 --> PC4
```

### 🟢 VLAN 10 — Finance
`PC1` • `PC2` • Gateway `192.168.10.1`

### 🔵 VLAN 20 — Engineering
`PC3` • `PC4` • Gateway `192.168.20.1`

---

## 🔧 Troubleshooting Challenge

**Symptom:** One Finance workstation suddenly loses connectivity while other users remain online.

<details>
<summary><b>🔍 View Diagnosis</b></summary>

The affected switch port was assigned to the wrong VLAN.

```text
SW2 Fa0/5 → VLAN 1 ❌
SW2 Fa0/5 → VLAN 10 ✅
```

Commands used:

```bash
show interfaces status
show vlan brief
show interfaces trunk
ping
```

</details>

<details>
<summary><b>🛠️ View Fix</b></summary>

```cisco
configure terminal
interface fa0/5
switchport access vlan 10
end
```

Connectivity was verified with:

```text
PC1 → Gateway     ✅
PC1 → PC2         ✅
PC1 → VLAN 20     ✅
```

</details>

---

## 📂 Packet Tracer Files

| File | Description |
|---|---|
| `01-baseline.pkt` | ✅ Fully operational network |
| `01-broken.pkt` | ❌ VLAN misconfiguration |
| `01-resolved.pkt` | 🔧 Troubleshot and restored |

> 💡 Download the `.pkt` files and open them with Cisco Packet Tracer to explore the network yourself.

---

### 🧠 Skills Demonstrated

`Cisco IOS` • `VLANs` • `802.1Q` • `Router-on-a-Stick` • `Inter-VLAN Routing` • `Layer 2 Troubleshooting`
