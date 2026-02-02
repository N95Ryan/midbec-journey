# 🔍 Audit Infrastructure Midbec

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

- [[tech-stack]] - Stack technique détaillée Midbec
- [[mission-overview]] - Contexte global de ma mission
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
**Statut actuel** : Audit terminé, recommandations documentées, en attente validation business pour priorisation