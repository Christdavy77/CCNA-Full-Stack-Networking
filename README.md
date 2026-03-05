# 🌐 Évolution d'une Architecture Réseau Cisco (CCNA)

Ce projet retrace la conception d'une infrastructure réseau d'entreprise, évoluant d'une configuration segmentée à une architecture hautement disponible et sécurisée.

## 📁 Accès aux Fichiers Packet Tracer
- [📥 Architecture de Base (TP2)](./TP2_Base_Infrastructure.pkt)
- [📥 Architecture Finale Haute Disponibilité (TP3)](./TP3_Architecture_Finale.pkt)

---

## 🛠️ Phase 1 : Fondations (TP2)
Mise en place de la segmentation et de la performance :
- **VLANs 10 (Compta) & 20 (Ventes)** : Isolation du trafic par service.
- **EtherChannel (PAgP)** : Agrégation de liens entre les switches de distribution.
- **Routage Inter-VLAN** : Configuration de SVI sur switch Layer 3.

---

## 🚀 Phase 2 : Expertise & Sécurité (TP3)
Optimisation pour une disponibilité critique et protection contre les attaques de couche 2.

### 🔄 Redondance de Passerelle (HSRP)
Mise en œuvre du protocole **HSRP (Hot Standby Router Protocol)** pour garantir une continuité de service.
- **IP Virtuelle (VIP) :** `192.168.10.254` et `192.168.20.254`.
- **Fonctionnement :** DSW1 est "Active". Si DSW1 tombe, DSW2 ("Standby") reprend le trafic instantanément.

### 🛡️ Sécurité DHCP (DHCP Snooping)
Protection du réseau contre les serveurs DHCP pirates (Rogue DHCP). Seuls les ports Trunks vers le cœur de réseau sont configurés en mode **Trusted**.

---

## 📸 Preuves de Fonctionnement
1. **Topologie Réseau complète** : ![Topologie](./01_topologie.png)
2. **Validation de l'EtherChannel** : ![EtherChannel Status](./02_etherchannel.png)
3. **État de la Redondance HSRP (TP3)** : ![HSRP Status](./03_interfaces_vlan.png)
4. **Test de Connectivité (Ping Inter-VLAN)** : ![Ping Final](./04_ping_final.png)

---

## 🚀 Commandes de Configuration Clés

### Activation du Routage et EtherChannel (DSW1)
```bash
# Activation du routage IP
DSW1(config)# ip routing

# Configuration de l'EtherChannel
DSW1(config)# interface range fa0/1 - 2
DSW1(config-if-range)# channel-group 1 mode desirable
DSW1(config-if-range)# switchport mode trunk


# Configuration pour le VLAN 10
DSW1(config)# interface vlan 10
DSW1(config-if)# standby 10 ip 192.168.10.254
DSW1(config-if)# standby 10 priority 110
DSW1(config-if)# standby 10 preempt

# Configuration pour le VLAN 20
DSW1(config)# interface vlan 20
DSW1(config-if)# standby 20 ip 192.168.20.254
DSW1(config-if)# standby 20 priority 110
DSW1(config-if)# standby 20 preempt


# Activation globale
ASW1(config)# ip dhcp snooping
ASW1(config)# ip dhcp snooping vlan 10,20

# Configuration du port de confiance (Trunk vers DSW)
ASW1(config)# interface fastEthernet 0/1
ASW1(config-if)# ip dhcp snooping trust

```
Auteur : Christdavy77

Statut : Projet CCNA Finalisé - Redondance & Sécurité validées.
