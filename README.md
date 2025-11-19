## Overview
This repository contains Zabbix templates for monitoring:
- **Cisco Access Points (AP)** via SNMP
- **Cisco Catalyst 9800 Wireless Controller** via SNMP
- **Cisco Inventory** via SNMP
- **ICMP Ping** for availability checks

These templates are designed to:
- Collect device status and inventory metrics
- Monitor availability and performance
- Gather information about clients, interfaces, and power
- Process SNMP traps for events (e.g., channel changes, DFS detection, AP disassociation)

---

## Features

### ✅ Cisco AP by SNMP
- **Inventory**: MAC addresses, serial number, model, software version, location
- **Status**: Operation Status, Uptime, Last Reboot Reason, Power Status
- **Network**: Ethernet Duplex, Link Speed, IP address
- **Clients**: Client Count
- **Availability**: ICMP ping, loss, response time
- **Triggers**:
  - AP unavailable via ICMP (HIGH)
  - Ethernet not in full duplex (AVERAGE)
  - Link speed decreased (AVERAGE)
  - Serial number changed (INFO)

### ✅ Cisco Catalyst 9800 by SNMP
- **Inventory**: Number of APs, supported AP limit
- **Network**: Rogue AP/Client Count
- **WLAN**: SSID status, client count
- **HA**: Hot Standby status
- **SNMP Traps**:
  - Channel change
  - DFS detection
  - AP disassociation
- **Triggers**:
  - Maximum AP join limit reached
  - HA status changed
  - DFS and channel events

### ✅ Cisco Inventory SNMP
- Hardware model and serial number
- Operating system details
- Entity serial number discovery

### ✅ ICMP Ping
- Basic availability checks
- Triggers for high loss and response time

---

## Requirements
- **Zabbix**: 6.0 LTS or higher (template created for 7.4)
- **Cisco IOS-XE**: 17.11+ for Catalyst 9800
- SNMP access to devices
- SNMPv3 recommended for security

---

## Used MIBs
- AIRESPACE-WIRELESS-MIB
- CISCO-LWAPP-AP-MIB
- CISCO-LWAPP-WLAN-MIB
- ENTITY-MIB
- SNMPv2-MIB  
Full list: [Cisco MIBs](https://github.com/cisco/cisco-mibs)

---

## Import Instructions
1. In Zabbix: **Configuration → Templates → Import**
2. Upload `zbx_export_templates.yaml`
3. Link the template to hosts (AP or controller)
4. Configure SNMP parameters and macros:
   - `{$ICMP_LOSS_WARN}` (default: 30%)
   - `{$ICMP_RESPONSE_TIME_WARN}` (default: 0.3s)

---
