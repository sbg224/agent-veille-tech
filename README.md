# veille-tech

Script Python de veille technique personnalisée — IA/LLM, réseaux & CCNA, offres d'emploi secteur tech.  
Déployé en service systemd sur VM dédiée (Debian 12), deux notifications Telegram par jour.

---

## Fonctionnement

```
[Script Python]
      │
      ├── Collecte de sources (flux RSS + APIs)
      │       └── Sujets ciblés :
      │           IA & LLM · Cisco / réseaux · offres d'emploi tech
      │
      ├── Analyse et synthèse via API Anthropic (Claude)
      │       └── Résumé contextuel + action concrète recommandée
      │
      └── Envoi via Telegram Bot
              └── Notification à 09h00 et 21h00
```

---

## Exemple de notification

```
🌅 Briefing Veille — 29/05/2026 à 09:01

🤖 IA & LLM
Claude Opus 4.8 maintenant sur Zot → comparer les coûts API vs usage actuel.
Package claude-hook-utils sur GitHub : hooks Python custom pour étendre Claude.

🌐 Réseau & CCNA
Zero Trust : article Network World sur les erreurs d'implémentation courantes.
Cisco Live 2026 Las Vegas : Cisco U. Theater annoncé.

⚡ Action du jour
Tester claude-hook-utils (1h) : hook qui génère les modèles Prisma depuis descriptions texte.
```

---

## Stack technique

| Composant | Détail |
|---|---|
| Langage | Python 3 |
| LLM | API Anthropic (Claude) — synthèse et analyse |
| Sources | Flux RSS + APIs publiques |
| Notification | Telegram Bot API |
| Déploiement | Service systemd sur Debian 12 |
| Planification | 09h00 et 21h00 — timer systemd |

---

## Structure du projet

```
veille-tech/
├── agent.py             # Orchestration principale — collecte, synthèse, envoi
├── tools.py             # Outils : sources RSS, APIs, formatage
├── config.py            # Tokens et paramètres (hors repo)
├── derniere_veille.json # Cache de la dernière exécution
└── README.md
```

---

## Déploiement

### 1. Configurer

Renseigner les tokens dans `config.py` (Anthropic + Telegram).

> ⚠️ Ne jamais commiter `config.py` — il est dans `.gitignore`

### 2. Déployer comme service systemd

```bash
sudo cp veille-tech.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable veille-tech
sudo systemctl start veille-tech
```

### 3. Vérifier

```bash
sudo systemctl status veille-tech
journalctl -u veille-tech -f
```

---

## Sécurité

- Aucune clé API ni token dans le code source
- Toute la configuration sensible est dans `config.py` (exclu du repo via `.gitignore`)
- Déployé sur VM isolée, accessible uniquement via VPN WireGuard

---

## Environnement de déploiement

- VM 104 (VMIA) — Debian 12 sur Proxmox VE
- VLAN 30 — automatisation & scripts
- Accessible uniquement via VPN WireGuard

---

![Python](https://img.shields.io/badge/Python-3.x-informational?style=flat&logo=python&color=3776AB)
![Anthropic](https://img.shields.io/badge/Anthropic-Claude_API-informational?style=flat&color=D97706)
![Telegram](https://img.shields.io/badge/Telegram-Bot_API-informational?style=flat&logo=telegram&color=26A5E4)
![systemd](https://img.shields.io/badge/systemd-service-informational?style=flat&logo=linux&color=4EAA25)
![Debian](https://img.shields.io/badge/Debian-12-informational?style=flat&logo=debian&color=A81D33)

---

*Projet personnel — infrastructure Toulouse*  
[LinkedIn](https://www.linkedin.com/in/mohamed-bah-aa38a1232/) · [GitHub](https://github.com/sbg224)
