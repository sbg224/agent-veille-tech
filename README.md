# veille-tech

Script Python de veille technique automatisée — réseaux, Cisco, cybersécurité, infrastructure.  
Déployé en service systemd sur VM dédiée (Debian 12).

---

## Fonctionnement

```
[Script Python]
      │
      ├── Interroge une API externe
      │       └── Récupère des informations techniques ciblées :
      │           réseaux · Cisco · cybersécurité · infrastructure
      │
      ├── Traitement et mise en forme des résultats
      │
      └── Envoi automatique via Telegram Bot
              └── Notification sur mobile / desktop
```

---

## Stack technique

| Composant | Détail |
|---|---|
| Langage | Python 3 |
| API | API externe (interrogation HTTP) |
| Notification | Telegram Bot API |
| Déploiement | Service systemd sur Debian 12 |
| Planification | Exécution automatique (cron / timer systemd) |

---

## Structure du projet

```
veille-tech/
├── main.py              # Script principal
├── config.py            # Configuration (tokens, paramètres)
├── requirements.txt     # Dépendances Python
├── veille-tech.service  # Fichier service systemd
└── README.md
```

---

## Installation

### 1. Cloner le repo

```bash
git clone https://github.com/sbg224/veille-tech.git
cd veille-tech
```

### 2. Installer les dépendances

```bash
pip install -r requirements.txt
```

### 3. Configurer

```bash
cp config.example.py config.py
# Editer config.py : renseigner les tokens API et Telegram
```

> ⚠️ Ne jamais commiter `config.py` — il est dans `.gitignore`

### 4. Déployer comme service systemd

```bash
sudo cp veille-tech.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable veille-tech
sudo systemctl start veille-tech
```

### 5. Vérifier

```bash
sudo systemctl status veille-tech
journalctl -u veille-tech -f
```

---

## Configuration Telegram Bot

1. Créer un bot via [@BotFather](https://t.me/botfather) sur Telegram
2. Récupérer le token
3. Obtenir son `chat_id`
4. Renseigner dans `config.py`

---

## Sécurité

- Aucune clé API ni token dans le code source
- Toute la configuration sensible est dans `config.py` (exclu du repo)
- Déployé sur VLAN isolé (VLAN 30 — automatisation)

---

## Environnement de déploiement

- VM Debian 12 sur Proxmox VE
- VLAN 30 (automatisation & scripts)
- Accessible uniquement via VPN WireGuard

---

![Python](https://img.shields.io/badge/Python-3.x-informational?style=flat&logo=python&color=3776AB)
![Telegram](https://img.shields.io/badge/Telegram-Bot_API-informational?style=flat&logo=telegram&color=26A5E4)
![systemd](https://img.shields.io/badge/systemd-service-informational?style=flat&logo=linux&color=4EAA25)
![Debian](https://img.shields.io/badge/Debian-12-informational?style=flat&logo=debian&color=A81D33)

---

*Projet personnel — infrastructure Toulouse*  
[LinkedIn](https://www.linkedin.com/in/mohamed-bah-aa38a1232/) · [GitHub](https://github.com/sbg224)
