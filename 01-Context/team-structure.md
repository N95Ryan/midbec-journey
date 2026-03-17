# 👥 Structure équipe — Midbec

**Contexte** : Mission modernisation site web (PHP → React). Deux piliers techniques principaux.

---

## 1. Patrick — Admin Système / DevOps

**Rôle** : Infrastructure, sécurité, déploiements.

### Responsabilités
- **Infrastructure** : serveurs, VPN, environnements (dev/staging/prod)
- **Sécurité système** : SSH, firewall, monitoring, bonnes pratiques
- **Support DevOps** : CI/CD, pipelines, déploiements
- **Disponibilité & stabilité** : garantie que l’infra supporte l’application

### Points de contact
- Décisions techniques conjointes (dev ↔ ops)
- Setup et évolution des environnements
- Accès, credentials, accès API / ERP

---

## 2. Moi — Software Engineer (Solo Developer)

**Rôle** : Couche applicative complète (frontend + intégrations backend).

### Responsabilités
- **Frontend** : migration PHP 5.6 → React, UI/UX, performances, SEO, accessibilité
- **Backend / intégrations** : API ERP Ogasys, API intermédiaire Python, garanties Whirlpool
- **Architecture** : choix stack, stratégie de migration, scalabilité (500k → 600k+ pièces)
- **Qualité & process** : documentation, tests, transition progressive, zéro downtime

### Collaboration
- **Avec Patrick** : infra, déploiements, sécurité, environnements
- **Avec équipes internes** : recueil besoins, priorisation, tests utilisateurs, formation

---

## Relation de travail

| Aspect            | Patrick (Admin Sys)     | Toi (Solo Dev)              |
| ----------------- | ----------------------- | --------------------------- |
| Périmètre         | Infra, sécurité, Ops    | App, frontend, intégrations |
| Décisions         | Conjointes (technique)  | Conjointes (technique)      |
| Livrables communs | Environnements, CI/CD   | App déployable, monitoring  |

**Objectif** : une seule équipe technique (dev + ops) pour livrer et maintenir le nouveau site.

---

**Liens** : [[mission-overview]] · [[tech-stack]]
