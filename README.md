# 🌐 Projet CCNA : Infrastructure Réseau Redondante & Routage Inter-VLAN

## 📌 Présentation du Projet
Ce TP simule une infrastructure d'entreprise hautement disponible. L'objectif est de segmenter le réseau en VLANs tout en garantissant une communication fluide entre les services via un switch de distribution (L3) et une agrégation de liens sécurisée.

## 🛠️ Concepts Mis en Œuvre
- **EtherChannel (PAgP)** : Agrégation de deux interfaces Gigabit pour la redondance et la performance.
- **Routage Inter-VLAN (SVI)** : Utilisation d'interfaces virtuelles sur le switch DSW1 pour le routage entre réseaux.
- **Trunking & Native VLAN** : Configuration des liens inter-switches avec le VLAN 99 pour la sécurité.

## 📸 Preuves de Fonctionnement

### 1. Topologie Réseau complète
![Topologie](./01_topologie.png)
*Vue d'ensemble montrant tous les liens opérationnels (pastilles vertes).*

### 2. Validation de l'EtherChannel
Vérification que le groupe `Po1` est en état **SU** (Layer2 / In Use) :
![EtherChannel Status](./02_etherchannel.png)

### 3. Interfaces de Routage (SVI)
Preuve que les passerelles VLAN 10 et 20 sont actives (Up/Up) :
![Interfaces](./03_interfaces_vlan.png)

### 4. Test de Connectivité (Ping Inter-VLAN)
Succès du ping entre le PC-Compta (192.168.10.10) et le PC-Ventes (192.168.20.10) :
![Ping Final](./04_ping_final.png)

## 🚀 Commandes de Configuration Clés
### Activation du routage (DSW1)
```bash
DSW1(config)# ip routing
DSW1(config-if)# interface vlan 10
DSW1(config-if)# ip address 192.168.10.1 255.255.255.0
