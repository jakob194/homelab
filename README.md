# Ubuntu Homelab: Self-Hosting

Mein privater Home-Server auf Basis von Ubuntu Server, der auf einem gebrauchten Laptop läuft. Er hostet mehrere Dienste in Docker-Containern. Der Zugriff von außen läuft ausschließlich über ein Tailscale-VPN, ohne Port-Forwarding und ohne öffentlich erreichbaren Reverse Proxy.

##️ Hardware & System

| | |
|---|---|
| **Gerät** | Dell Latitude 3570 (gebraucht) |
| **CPU** | Intel Core i5 |
| **RAM** | 8 GB |
| **Speicher** | SSD (nachgerüstet), 1 TB |
| **OS** | Ubuntu Server [Version, z. B. 24.04 LTS] |

## Applications (Docker)

| **Immich** | Foto- und Video-Backup |
| **Nextcloud** | Private Cloud für Dateien und Synchronisation |
| **Jellyfin** | Medienserver für Filme und Serien |
| **Audiobookshelf** | Hörbücher |
| **Pi-hole** | DNS-Server mit Ad- und Tracker-Blocking |
| **Portainer** | Weboberfläche zur Verwaltung der Container |

Verwaltet wird alles mit [Docker Compose / Portainer-Stacks]. Die Konfigurationen liegen im Ordner

## Netzwerk & Zugriff

Statt Dienste per Reverse Proxy und Portfreigabe ins Internet zu stellen, habe ich mich bewusst für **Tailscale** (WireGuard-basiertes Mesh-VPN) entschieden. Ein Reverse Proxy wäre eine zusätzliche Angriffsfläche, besonders bei privaten Daten wie Fotos und Cloud-Dateien.

- **Keine Portfreigaben am Router:** Der Server ist aus dem Internet nicht direkt erreichbar. Zugriff haben nur Geräte in meinem Tailnet.
- **Pi-hole als DNS im Tailnet:** Pi-hole ist in Tailscale als DNS-Server eingetragen. Smartphone und Laptop blocken Werbung und Tracker deshalb auch im Mobilfunknetz oder in fremden WLANs.
- **Exit Node:** Der Server ist als Exit Node eingerichtet. Unterwegs kann ich meinen gesamten Datenverkehr über mein Heimnetz leiten, meine Grundidee war einen eigenen VPN zu erstellen.
Für den Exit Node muss IP-Forwarding im Kernel aktiviert sein:

## Absicherung

- Zugriff von außen nur über Tailscale, keine offenen Ports am Router
- [SSH: nur Key-Login, Root-Login deaktiviert]
- [Firewall: UFW, eingehend standardmäßig gesperrt]
- [Automatische Sicherheitsupdates: unattended-upgrades]

## Backups

Automatischer backup täglicher Backup auf den WD My Cloud Single-Bay (1st Generation) mit 3TB 

## Was ich für Grundlagen gelernt habe

- Linux-Administration: Installation, Benutzer und Rechte, Dienste, Logs
- Docker: Multi-Container-Setups, Volumes, Container-Netzwerke
- Netzwerk: VPN-Konzepte, DNS, IP-Forwarding, Verzicht auf öffentliche Angriffsfläche
- Troubleshooting: Fehlersuche bei Containern, DNS und Routing
