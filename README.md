# Réseau d'Entreprise Sécurisé — VLAN + Routage + Supervision

![Topologie](schemas/topologie_physique.png)

## Présentation

Conception et déploiement complet d'un réseau d'entreprise multi-VLAN
sécurisé, simulé sous **Cisco Packet Tracer.  
Projet personnel realisé dans le cadre d'aquisition de competence, Abidjan.



## Architecture réseau

| Équipement | Modèle | Rôle |
|------------|--------|------|
| Routeur (KANATE) | Cisco 2911 | Passerelle Internet |
| Switch L3 (IBRA) | Cisco 3560-24PS | Routage inter-VLAN |
| Switch L2 (Moon) | Cisco 2960-24TT | Accès VLAN 10 & 20 |
| Switch L2 (Diak) | Cisco 2960-24TT | Accès VLAN 30 & 40 |
| Server0 | Server-PT | DHCP · DNS · Syslog |



## Plan d'adressage

| VLAN | Nom | Réseau | Passerelle | Plage DHCP |
|------|-----|--------|------------|------------|
| 10 | Direction | 10.10.10.0/24 | 10.10.10.1 | .11 → .50 |
| 20 | Employés | 10.10.20.0/24 | 10.10.20.1 | .11 → .100 |
| 30 | Serveurs | 10.10.30.0/24 | 10.10.30.1 | Statique |
| 40 | DMZ | 10.10.40.0/24 | 10.10.40.1 | .11 → .50 |
| — | Lien P-à-P | 10.10.0.0/30 | — | SW-CORE .1 / Routeur .2 |


## Fonctionnalités implémentées

- VLANs 802.1Q : segmentation en 4 zones (Direction, Employés, Serveurs, DMZ)
- Trunk dot1Q : interconnexion Switch L3 ↔ Switches L2
- Routage inter-VLAN : Switch L3 avec interfaces SVI + ip routing
- DHCP centralisé : 4 pools + relay agent ip helper-address
- DNS : enregistrements A pour les ressources internes
- ACLs étendues : politique de cloisonnement par département
- Syslog : centralisation des journaux sur Server0 (UDP 514)
- SNMP v2c : monitoring des équipements réseau

---

## Politique de sécurité (ACLs)

| Source | Direction | Employés | Serveurs | DMZ | Internet |
|--------|-----------|----------|----------|-----|----------|
| Direction | ✓ | ✓ | ✓ | ✗ | ✓ |
| Employés | ✗ | ✓ | ✓ | ✗ | ✓ |
| Serveurs | ✓ | ✓ | ✓ | ✗ | ✗ |
| DMZ | ✗ | ✗ | ✗ | ✓ | ✓ |

---

## Contenu du dépôt


├── captures/       # Screenshots CLI et Packet Tracer
├── configs/        # Running-config de chaque équipement
├── schemas/        # Topologie et plan d'adressage
├── simulation/     # Fichier .pkt Packet Tracer
└── README.md


## Technologies

Cisco IOS` `VLAN 802.1Q` `Routage L3` `SVI` `DHCP Relay
DNS` `ACL étendues` `Syslog` `SNMP v2c` `Packet Tracer

## Auteur

BOURAIMA KANATE 
Diplomé d'un Master 2 — Électronique et Systèmes de Télécommunication  
Université Félix Houphouët-Boigny — Cocody, Abidjan, Côte d'Ivoire
