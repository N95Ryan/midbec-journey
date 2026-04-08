# 🎯 Mission Midbec - Vue d'ensemble

**Titre** : Software Engineer (Solo Developer)  
**Localisation** : Midbec, Canada  
**Status actuel** : Mission en cours (Permis de travail validé)

---

## 📅 Timeline

| Date                    | Événement                                             |
| ----------------------- | ----------------------------------------------------- |
| **8 Octobre 2025**      | Entretien + rencontre équipe complète                 |
| **Oct-Déc 2025**        | Acceptation offre + démarches permis travail          |
| **Fév 2026**            | Audit technique préparatoire (pendant attente permis) |
| **Mars 2026**           | 🚀 Début officiel mission                            |

---

## 🎯 Mission principale

### Objectif business
**Modernisation complète du site web Midbec** : migration stack legacy (PHP 5.6) vers architecture moderne et scalable (Next.js / Go).

### Pourquoi cette mission ?
- Stack actuelle **obsolète et critique** (PHP 5.6 EOL depuis 2018)
- Risques **sécurité, performance, maintenabilité**
- Besoin **scalabilité** pour croissance inventaire (500k → +2m pièces)
- Améliorer **expérience utilisateur** et vitesse du site

---

## 🔧 Responsabilités techniques

### 1. Refonte frontend (priorité #1)
- **Migration complète** : PHP 5.6 legacy → **React** moderne
- **Réécriture UI/UX** : composants réutilisables, responsive
- **Optimisation performances** : bundle size, lazy loading, caching
- **SEO & accessibility** : conformité standards web

### 2. Intégration backend
- **API ERP Ogasys** : connexion inventaire massif (~500k pièces actuellement, 2m+ prévu)
- **Gestion données** : pagination, filtres, recherche performante
- **API intermédiaire Python** : maintenance/amélioration si nécessaire
- **Garanties Whirlpool** : intégration API spécialisée

### 3. Architecture & scalabilité
- **Choix techniques** : stack, outils, architecture globale
- **Modernisation progressive** : stratégie migration sans casser le prod
- **Performance** : optimisation requêtes, caching stratégique, CDN
- **Monitoring** : mise en place tracking performance, erreurs

### 4. Collaboration & transition
- **Travail avec Patrick (admin sys)** : infrastructure, déploiement, sécurité
- **Équipes internes** : recueil besoins, tests utilisateurs, formation
- **Transition progressive** : migration par phases, zéro downtime
- **Documentation** : code, architecture, processus pour futur

---

## 👥 Structure équipe

### Rôle actuel
**Solo developer** : responsable de toute la couche applicative (frontend + intégrations backend)

### Collaboration clé
**Patrick (Admin Sys)** :
- Gestion infrastructure (serveurs, VPN, déploiements)
- Sécurité système (SSH, firewall, monitoring)
- Support DevOps (CI/CD, environnements)

**Relation de travail** : Étroite collaboration dev ↔ ops, décisions techniques conjointes

### Équipes internes (stakeholders)
- **Business/Product** : validation fonctionnalités, priorisation
- **Utilisateurs finaux** : feedback UX, tests
- **Support client** : remontées bugs, demandes features

---

## 🎯 Objectifs mesurables (pour CV)

### Technique
- [ ] Migration **100% PHP → React** avec feature parity
- [ ] Réduction temps chargement de **X%** (baseline à établir)
- [ ] Support **600k+ pièces** avec temps réponse < 2s
- [ ] **Zéro downtime** pendant migration
- [ ] Mise en place **CI/CD pipeline** complet

### Architecture
- [ ] Architecture **scalable et maintenable** documentée
- [ ] **API design** optimisé pour performances
- [ ] **Sécurité renforcée** : audit + corrections vulnérabilités
- [ ] **Monitoring & alerting** opérationnels

### Process
- [ ] **Documentation complète** : code, architecture, runbooks
- [ ] **Tests automatisés** : couverture >80%
- [ ] **Onboarding process** pour futurs devs
- [ ] **Knowledge transfer** à l'équipe interne

### Business impact
- [ ] Amélioration **satisfaction utilisateur** (metrics à définir)
- [ ] Réduction **coûts maintenance** (moins de hotfixes)
- [ ] **Time-to-market** features réduit grâce à stack moderne
- [ ] **Sécurité renforcée** : réduction surface d'attaque

---

## 🚀 Phases projet (draft)

### Phase 0 : Préparation (Oct 2024 - Jan 2026)
- ✅ Audit infrastructure (voir section « Audit infrastructure » ci-dessous)
- ⏳ Analyse besoins fonctionnels
- ⏳ POC React + API Ogasys
- ⏳ Architecture cible validée

### Phase 1 : Foundation (mois 1-2)
- [ ] Setup environnement dev/staging
- [ ] Boilerplate Next.js + tooling (Vite, TypeScript, Tailwind)
- [ ] Authentification & routing de base
- [ ] Connexion API Ogasys (read-only d'abord)

### Phase 2 : Core features (mois 3-5)
- [ ] Catalogue produits (avec 500k pièces)
- [ ] Recherche & filtres performants
- [ ] Pages détail produit
- [ ] Panier & checkout (si applicable)

### Phase 3 : Advanced (mois 6-8)
- [ ] Features spécifiques métier
- [ ] Intégration garanties Whirlpool
- [ ] Optimisations performance poussées
- [ ] Migration données/utilisateurs

### Phase 4 : Go-live (mois 9-10)
- [ ] Tests intensifs (QA, load testing)
- [ ] Migration DNS progressive (canary)
- [ ] Monitoring production
- [ ] Support post-launch

### Phase 5 : Amélioration continue (mois 11+)
- [ ] Analyse métriques, optimisations
- [ ] Nouvelles features basées sur feedback
- [ ] Documentation finale & knowledge transfer

**Note** : Timeline indicative, à ajuster selon réalités terrain

---

## 🔗 Liens connexes

- Section « Audit infrastructure » ci-dessous — État des lieux technique initial
- [[stack]] - Stack technique complète
- [[patrick]] · [[ryan]] · [[charles-etienne]] — Organigramme détaillé
- [[migration-react]] - Détails projet migration (à créer)
- [[technical-debt]] - Dette technique à adresser
- [[security-concerns]] - Risques sécurité identifiés

---

## 🧠 Défis anticipés

### Technique
- **Migration progressive** : garder ancien site fonctionnel pendant transition
- **Performance** : 500k+ pièces = enjeu caching/pagination/indexation
- **API Ogasys** : documentation limitée, comportement "non-standard"
- **Solo dev** : responsabilité complète stack, pas de pair programming

### Process
- **Attente permis** : délai incertain, peut décaler timeline
- **Stack legacy** : 7+ ans de dette technique à gérer
- **Environnements** : pas de staging actuellement = risque déploiements
- **Documentation** : quasi inexistante, découverte au fil de l'eau

### Business
- **Transition utilisateurs** : changement UI peut créer résistance
- **Priorisation features** : équilibrer migration vs nouvelles demandes
- **Zéro downtime** : contrainte forte pour site e-commerce (si applicable)

---

## 💪 Opportunités

### Pour Midbec
- **Modernisation** : stack 2026 vs 2018 = 8 ans de gains techno
- **Scalabilité** : prêt pour croissance 600k+ pièces et au-delà
- **Maintenabilité** : code propre, testé, documenté
- **Sécurité** : élimination vulnérabilités critiques

### Pour moi (CV senior Toronto)
- **Ownership complet** : architecture, décisions, implémentation
- **Scale** : gérer 500k+ records en production
- **Migration legacy** : expérience complète modernisation stack
- **Solo leadership** : autonomie, collaboration cross-fonctionnelle
- **Impact mesurable** : avant/après quantifiable

---

## 📝 Notes additionnelles

### Pourquoi cet audit pré-démarrage ?
- **Anticipation** : comprendre terrain avant arrivée officielle
- **Préparation** : POC, décisions architecturales éclairées
- **Efficacité** : hit the ground running dès jour 1
- **Professionalism** : montre initiative et sérieux

### Stratégie permis de travail
- **Timing incertain** : peut prendre quelques semaines à quelques mois
- **Utilisation du temps** : audit technique = préparation productive
- **Risque** : si permis retardé, décalage timeline projet
- **Mitigation** : communication régulière avec Midbec sur avancement

---

**Dernière mise à jour** : 2025-01-31  
**Prochaine révision** : Après réception permis de travail\n\n---\n\n# 🔍 Audit Infrastructure Midbec

**Date de début** : Janvier 2026  
**Status** : ✅ Complété (phase initiale)  
**Impact CV** : Architecture legacy, Sécurité, Dette technique, Scalabilité

## 🎯 Contexte & Mission

**Objectif** : Audit complet de l'infrastructure existante avant migration frontend React.

**Déclencheur** : Besoin de comprendre l'architecture actuelle pour planifier la modernisation.

**Périmètre** : Stack technique, risques sécurité, points de défaillance, scalabilité.

---

## 🔧 Stack technique identifiée

| Composant | Technologie | Localisation | État | Niveau de risque |
|-----------|-------------|--------------|------|------------------|
| **Frontend legacy** | PHP 5.6 | Ubuntu `/var/www/html/live.midbec.com` | ⚠️ EOL 2018 | 🔴 CRITIQUE |
| **Frontend nouveau** | React | À développer | 🚧 En projet | - |
| **ETL/API intermédiaire** | Python | `192.168.200.57:5000` | ⚠️ SPOF | 🟠 ÉLEVÉ |
| **ERP** | Ogasys | `10.10.10.201:8088` | API non-standard | 🟡 MOYEN |
| **CMS** | Custom (Loginov) | Gère PHP 5.6 | Legacy opaque | 🟡 MOYEN |
| **CDN/DNS** | Cloudflare | Toutes les requêtes sauf Whirlpool | SPOF | 🟡 MOYEN |
| **API spécialisée** | ? | Garanties Whirlpool | Non documentée | 🟡 À explorer |
| **VPN** | WireGuard | Accès infrastructure | ✅ Bon choix | 🟢 OK |

**Volume de données** : ~500k pièces en inventaire ERP → **Enjeu scalabilité majeur**

---

## 🚨 Risques critiques identifiés

### 1. 🔐 Sécurité

#### Obsolescence critique
- **PHP 5.6** : EOL depuis **2018** = 7 ans de vulnérabilités non patchées
- **Ubuntu 18.04** : Fin de support standard avril **2023**
- **Surface d'attaque massive** sans mises à jour possibles

#### Authentification faible
- **SSH** : authentification par **mot de passe uniquement**
  - ❌ Pas de clés SSH
  - ❌ Pas de 2FA/MFA
  - ⚠️ Exposition brute-force
  
- **API Ogasys** : header d'auth simpliste
```
  Key: 23rsadf3ytgWFRER65
```
  - ❌ Pas de rotation de clés
  - ❌ Pas de rate limiting apparent
  - ⚠️ Risque d'abus/surcharge

#### Infrastructure exposée
- ❌ Pas de WAF (Web Application Firewall) devant les services
- ❌ Pas de logs centralisés visibles
- ❌ Pas de monitoring/alertes configurés

### 2. 💾 Infrastructure fragile

#### Saturation imminente
- **Disque `/var/www` à 85.3%**
  - ⚠️ Risque de crash applicatif
  - ❌ Pas d'alertes configurées
  - ❌ Pas de stratégie de purge/archivage

#### Points de défaillance uniques (SPOF)
- **ETL Python** : aucune redondance
  - Si ce service tombe → toute la chaîne de transformation s'arrête
  - Pas de fallback apparent
  
- **Cloudflare** : single point of failure pour DNS/CDN
  - Si panne Cloudflare → site inaccessible

#### Pas d'environnements isolés
- ❌ Pas d'env dev/staging identifié
- ⚠️ **Déploiement = édition directe en production**
- 🔥 Une erreur = tout casse, zéro filet de sécurité

### 3. ⚡ Scalabilité compromise

#### Volume croissant non géré
- **500k → 600k pièces** sans stratégie adaptée :
  - ❌ Pas de **pagination** implémentée
  - ❌ Pas de **caching** côté serveur
  - ❌ Pas de stratégie d'**indexation** pour recherches
  - ⚠️ Risque de **timeouts** sur requêtes lourdes

#### API Ogasys mystérieuse
- Documentation incomplète (endpoint `/test/...` seulement)
- Comportement "étrange & non-standard" (selon notes internes)
- Risque d'effets de bord non anticipés

---

## 🔧 Anti-patterns & problèmes process

### ❌ Configuration VPN non testée (Day 1)

**Fichier `.conf` WireGuard cassé à la livraison** :
```conf
# ❌ Erreurs détectées
Address = 192.168.200/24      # IP incomplète (manque .X)
AllowedIPs = 192.168.200/24   # IP incomplète
# Réseau 10.10.11.0/24 absent alors que mon IP = 10.10.11.31/32
```

**Fix appliqué** :
- Corrections manuelles des IPs
- Ajout réseau `10.10.11.0/24` manquant

**Impact** : ~30 min de debugging évitable

**Red flag détecté** : 
- ❌ Pas de validation/QA avant envoi aux développeurs
- ❌ Manque de process de vérification
- ⚠️ Risque de répétition pour futurs collaborateurs

### ❌ Dev experience limitée

- 🔧 CLI uniquement pour accéder au code (pas de Remote Dev setup type VS Code)
- 🔧 Pas de documentation claire sur l'architecture globale
- 🔧 Pas de Git workflow défini/documenté
- 🔧 Onboarding technique inexistant

---

## 💡 Décisions & recommandations techniques

### 🔐 Sécurité (priorité HAUTE)

#### Immédiat
- [ ] **Migration SSH** : clés ED25519 + désactivation auth par password
- [ ] **Rotation clé API** Ogasys + mise en place rotation automatique
- [ ] **Setup monitoring disque** + alertes à 80%, 90%, 95%
- [ ] **Audit logs** : centralisation + monitoring événements suspects

#### Court terme
- [ ] **WAF** devant services exposés (Cloudflare ou équivalent)
- [ ] **Rate limiting** API Ogasys
- [ ] **Plan migration PHP 5.6** → stack moderne (React déjà prévu)
- [ ] **Upgrade Ubuntu** 18.04 → LTS supportée

### 🏗️ Architecture (priorité MOYENNE)

- [ ] **Env staging** : clone prod pour tester déploiements
- [ ] **Redondance ETL Python** : failover ou queue système
- [ ] **Documentation API Ogasys** : explorer endpoints, comportements, limites
- [ ] **Strategy CDN** : évaluer alternatives/backup à Cloudflare

### ⚡ Scalabilité (priorité HAUTE)

- [ ] **Pagination API** : implémenter pour requêtes 500k+ records
- [ ] **Caching stratégique** :
  - Redis/Memcached côté serveur
  - Cache-Control headers optimisés
- [ ] **Indexation DB** : analyser queries lentes, optimiser indexes
- [ ] **Load testing** : simuler 600k+ pièces pour identifier bottlenecks

### 📋 Process (priorité MOYENNE)

- [ ] **Checklist validation config** avant envoi aux devs
- [ ] **Documentation architecture** : schémas, flows, dépendances
- [ ] **Git workflow** : branching strategy, code review process
- [ ] **Onboarding doc** : setup dev, accès VPN, ressources clés

---

## 📊 Impact mesurable (pour CV senior)

### Audit & analyse
- ✅ **Audit complet** infrastructure legacy multi-composants
- ✅ Identification de **15+ vulnérabilités critiques** (PHP EOL, SSH faible, SPOF)
- ✅ Évaluation risques sécurité/scalabilité sur **500k+ records**

### Architecture & propositions
- ✅ **Cartographie** stack technique complète (8 composants)
- ✅ **Recommandations priorisées** sécurité/architecture/scalabilité
- ✅ Détection **single points of failure** + propositions redondance

### Leadership technique
- ✅ **Documentation dette technique** pour priorisation business
- ✅ **Roadmap sécurité** court/moyen terme
- ✅ Identification gaps **process/QA** + recommandations

**Compétences démontrées** :
- Architecture legacy assessment
- Security audit
- Scalability planning
- Technical documentation
- Risk assessment & prioritization

---

## 🔗 Liens connexes

- [[stack]] - Stack technique détaillée Midbec
- [[mission]] - Contexte global de ma mission
- [[technical-debt]] - Dette technique consolidée
- [[security-concerns]] - Préoccupations sécurité globales
- [[process-issues]] - Problèmes de process détectés
- [[migration-react]] - Projet migration frontend (à créer)

---

## 🧠 Apprentissages clés

### Technique
- **Audit infra legacy sans doc** : approche systématique composant par composant
- **Identification SPOF** : méthodologie de détection points critiques
- **Trade-offs sécurité vs vélocité** : réalités PME avec ressources limitées
- **EOL stack** : implications concrètes (PHP 5.6 = 7 ans de vulnérabilités)

### Architecture
- **Defense in depth** : VPN bien configuré ≠ sécurité globale
- **Scalabilité préventive** : anticiper 500k → 600k avant que ça casse
- **Documentation critique** : API "mystérieuse" = risque opérationnel majeur

### Process & soft skills
- **Importance QA** : config cassée = perte confiance + temps
- **Documentation proactive** : absence = onboarding chaotique
- **Communication risques** : priorisation claire pour décisions business

### Patterns détectés
- **Infra défensive mais dette technique massive** : sécurité périmétrique (VPN) OK, mais stack interne critique
- **SPOF multiples** : ETL, Cloudflare, pas d'env staging
- **Manque culture DevOps** : pas de monitoring, logs, alertes, CI/CD

---

## 📝 Prochaines étapes

### Investigation approfondie
1. [ ] **Explorer API Ogasys** en détail
   - Tous les endpoints disponibles (au-delà de `/test/...`)
   - Limites rate, comportements edge cases
   - Documentation complète pour l'équipe

2. [ ] **Évaluer effort migration PHP → React**
   - Inventaire fonctionnalités actuelles
   - Estimation complexité
   - Dépendances CMS Loginov

### Propositions business
3. [ ] **Roadmap sécurité priorisée** avec estimations
   - Quick wins (SSH keys, monitoring) vs long terme (migration PHP)
   - Coût vs risque de chaque item

4. [ ] **Architecture cible** pour nouvelle stack
   - Diagrammes avant/après
   - Plan de migration progressive
   - Stratégie zéro-downtime

---

**Dernière mise à jour** : 2025-01-31  
**Statut actuel** : Audit terminé, recommandations documentées, en attente validation business pour priorisation\n