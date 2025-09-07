# Dokumentasi Jaringan Server

## Ringkasan
Server ini memiliki beberapa interface jaringan aktif berdasarkan hasil `ifconfig`.  
Interface terbagi menjadi:

- **Interface fisik**: LAN (aktif), Wi-Fi (nonaktif).
- **Interface virtual**: Docker bridge, WireGuard, Tailscale, loopback.
- **Kontainer Docker**: terhubung ke berbagai network bridge (`br-xxxx`).

## Detail Interface

### Interface Fisik
- **LAN (enp3s0f2)**: `192.168.1.20/24`  
  → Interface utama untuk koneksi ke internet/LAN.  
- **Wi-Fi (wlp2s0)**: Tidak aktif.

### Loopback
- **lo**: `127.0.0.1`  
  → Komunikasi internal antar aplikasi dalam server.

### Docker
- **docker0**: `172.17.0.1/16` (default bridge)  
- Beberapa custom bridge:
  - br-1955bdeca4fc → `172.18.0.1`
  - br-2674075a9c1b → `172.23.0.1`
  - br-525fea672d18 → `172.22.0.1`
  - br-56e18e08920f → `172.24.0.1`
  - br-7da4494dfde9 → `172.20.0.1`
  - br-8cec9a14d87e → `172.26.0.1`
  - br-a47c0b428dc3 → `172.21.0.1`
  - br-c3c26e751091 → `172.25.0.1`
  - br-f17882ea7749 → `172.27.0.1`
  - br-f4706f414b66 → `172.19.0.1`

### VPN
- **WireGuard (wg0)**: `10.2.0.2`  
  → VPN aktif, banyak traffic (224 MB RX).  
- **Tailscale (tailscale0)**: `100.119.11.49`  
  → VPN overlay via WireGuard, sedikit traffic.

---

## Diagram Topologi
Berikut visualisasi topologi dari hasil `ifconfig`:

![Network Topology](Docs/network_topology.png)

---

## Kesimpulan
1. Jaringan utama: **LAN via enp3s0f2 (192.168.1.20)**  
2. **Wi-Fi tidak dipakai.**  
3. **Docker aktif**, dengan banyak bridge & kontainer.  
4. **VPN ganda**: WireGuard (aktif) & Tailscale (standby).  
5. Semua interface sehat, packet drop sangat kecil.

---
