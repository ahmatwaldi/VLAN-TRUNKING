# 🧪 Hari 2 - Simulasi VLAN dan Trunking (Router-on-a-Stick)

## 🎯 Tujuan
Simulasi ini bertujuan untuk melatih pemahaman dalam membangun segmentasi jaringan menggunakan VLAN, 
menghubungkan dua switch melalui trunking, dan menerapkan metode inter-VLAN routing 
dengan teknik **Router-on-a-Stick** pada perangkat Cisco.

---

## 🖥️ Topologi
- 1 Router (Router0)
- 2 Switch (Switch0 dan Switch1)
- 4 PC (PC0, PC1, PC2, PC3)

---

## 🧱 Desain VLAN
| Perangkat | VLAN | Nama VLAN | IP Address        |
|-----------|------|-----------|-------------------|
| PC0       | 10   | VLAN10    | 192.168.10.2/24   |
| PC1       | 10   | VLAN10    | 192.168.10.3/24   |
| PC2       | 20   | VLAN20    | 192.168.20.2/24   |
| PC3       | 20   | VLAN20    | 192.168.20.3/24   |

---

## ⚙️ Langkah Konfigurasi

🔸 Switch - VLAN & Access Port
- Switch 1 :
  vlan 10
  name HRD

  interface fa0/1
  switchport mode access
  switchport access vlan 10

  interface fa0/2
  switchport mode access
  switchport access vlan 10

-Switch 2 :
  vlan 20
  name VP

  interface fa0/1
  switchport mode access
  switchport access vlan 10

  interface fa0/2
  switchport mode access
  switchport access vlan 10

🔸 Trunk Antar Switch
  int fa0/3
  switchport mode trunk

🔸 Router-On-a-stick
  interface fa0/0
  no shutdown
  
  interface fa0/0.10
  encapsulation dot1Q 10
  ip address 192.168.10.1 255.255.255.0

  interface fa0/1
  no shutdown

  interface fa0/0.20
  encapsulation dot1Q 20
  ip address 192.168.20.1 255.255.255.0

🔸 Konfigurasi IP PC

| PC  | IP Address   | Subnet Mask   | Default Gateway |
| --- | ------------ | ------------- | --------------- |
| PC0 | 192.168.10.2 | 255.255.255.0 | 192.168.10.1    |
| PC1 | 192.168.10.3 | 255.255.255.0 | 192.168.10.1    |
| PC2 | 192.168.20.2 | 255.255.255.0 | 192.168.20.1    |
| PC3 | 192.168.20.3 | 255.255.255.0 | 192.168.20.1    |


🔸 Pengujian : SUCCESS
