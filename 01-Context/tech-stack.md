# 🛠️ Stack technique Midbec

**Dernière mise à jour** : 2025-01-31  
**Source** : Audit infrastructure initial

---

## 📊 Vue d'ensemble

### Stack actuelle (Legacy - à migrer)
```
┌─────────────────────────────────────────┐
│          Utilisateurs finaux            │
└─────────────────┬───────────────────────┘
                  │
         ┌────────▼────────┐
         │   Cloudflare    │ (CDN/DNS)
         │   (SPOF)        │
         └────────┬────────┘
                  │
    ┌─────────────▼──────────────┐
    │  Frontend Legacy           │
    │  PHP 5.6 + Ubuntu 18.04    │ ⚠️ CRITIQUE
    │  /var/www/html/...         │
    │  CMS: Loginov (custom)     │
    └─────────────┬──────────────┘
                  │
         ┌────────▼────────┐
         │  ETL Python     │
         │  192.168.200.57 │ (SPOF)
         │  Port 5000      │
         └────────┬────────┘
                  │
         ┌────────▼────────┐
         │   ERP Ogasys    │
         │   10.10.10.201  │ (~500k pièces)
         │   Port 8088     │
         └─────────────────┘
```

### Stack cible (Moderne - en cours)
```
┌─────────────────────────────────────────┐
│          Utilisateurs finaux            │
└─────────────────┬───────────────────────┘
                  │
         ┌────────▼────────┐
         │   Cloudflare    │ (CDN)
         └────────┬────────┘
                  │
    ┌─────────────▼──────────────┐
    │  Frontend Modern           │
    │  React + TypeScript        │ ✅ CIBLE
    │  Vite + Tailwind CSS       │
    │  Hosted: [À définir]       │
    └─────────────┬──────────────┘
                  │
         ┌────────▼────────┐
         │  API Layer      │ (À définir: Go? Node?)
         │  REST/GraphQL   │
         └────────┬────────┘
                  │
    ┌─────────────┴──────────────┐
    │                            │
┌───▼────┐              ┌────────▼────┐
│ Python │              │  ERP Ogasys │
│  ETL   │              │  (existing) │
└────────┘              └─────────────┘
```

---

## 🔧 Détail composants actuels

### Frontend Legacy

**Technologie** : PHP 5.6  
**OS** : Ubuntu 18.04  
**Localisation** : `/var/www/html/live.midbec.com`  
**CMS** : Custom (Loginov) - dépendance opaque  
**Disque** : ⚠️ 85.3% utilisé (saturation imminente)

**Problèmes** :
- ❌ EOL depuis **2018** (7 ans sans patch sécurité)
- ❌ Ubuntu 18.04 fin de support (avril 2023)
- ❌ Vulnérabilités critiques non corrigeables
- ❌ Performances limitées
- ❌ Maintenabilité difficile

**Liens** : [[infrastructure-audit#sécurité]]

### ETL/API Intermédiaire

**Technologie** : Python  
**Localisation** : `192.168.200.57:5000`  
**Rôle** : Transformation données entre frontend et ERP

**Problèmes** :
- ⚠️ **Single Point of Failure** (SPOF)
- ❌ Pas de redondance
- ❌ Pas de fallback si crash
- ⚠️ Documentation limitée

**Questions ouvertes** :
- Version Python ?
- Framework utilisé (Flask? FastAPI?) ?
- Logique métier incluse ?

### ERP Ogasys

**Technologie** : Ogasys (propriétaire)  
**Localisation** : `10.10.10.201:8088`  
**Données** : ~500k pièces inventaire (→ 600k prévu)

**API** :
- Endpoints connus : `/test/...` (documentation incomplète)
- Auth : `Key: 23rsadf3ytgWFRER65` (header simple)
- ⚠️ Comportement "étrange & non-standard" (notes internes)

**Problèmes** :
- ❌ Documentation API limitée
- ❌ Pas de rate limiting apparent
- ❌ Pas de rotation clé d'auth
- ⚠️ Scalabilité 500k+ records non testée

**À investiguer** :
- Tous les endpoints disponibles
- Limites requêtes (rate, payload)
- Stratégie pagination/filtres
- Support GraphQL ou REST uniquement ?

### CDN/DNS

**Technologie** : Cloudflare  
**Rôle** : CDN + DNS pour toutes les requêtes (sauf Whirlpool API)

**Problèmes** :
- ⚠️ Single Point of Failure pour DNS/CDN
- ❌ Pas de fallback identifié

**Avantages** :
- ✅ Protection DDoS
- ✅ SSL/TLS géré
- ✅ Cache global

### API Garanties Whirlpool

**Technologie** : ? (non documentée)  
**Rôle** : Gestion garanties produits Whirlpool  
**État** : À explorer et documenter

### VPN

**Technologie** : WireGuard  
**Rôle** : Accès sécurisé infrastructure interne

**État** : ✅ Bon choix technologique

**Problèmes détectés** :
- Config initiale cassée (IPs incomplètes) → [[infrastructure-audit#config-vpn-cassée]]
- Pas de QA avant livraison

---

## 🎯 Stack cible (Migration)

### Frontend

**Framework** : **React** (confirmé)  
**Language** : **TypeScript** (recommandé fort)  
**Build tool** : **Vite** (rapide, moderne)  
**Styling** : **Tailwind CSS** (utilité-first, productivité)  
**State** : **Zustand** ou **TanStack Query** (selon besoins)  
**Routing** : **React Router** ou **TanStack Router**

**Pourquoi ce choix** :
- ✅ React : écosystème mature, recrutement facile
- ✅ TypeScript : sécurité types, scalabilité
- ✅ Vite : build ultra-rapide, HMR performant
- ✅ Tailwind : productivité, consistency design
- ✅ TanStack Query : gestion data fetching/cache excellente pour APIs

**À définir** :
- [ ] Hosting (Vercel? Netlify? Railway? Render?)
- [ ] SSR/SSG nécessaire ? (Next.js vs Vite)
- [ ] Framework UI (shadcn? MUI? Custom?)

### Backend/API Layer

**Options à évaluer** :

#### Option 1 : Go (recommandé personnel)
- **Framework** : Gin, Echo, ou Fiber
- **Avantages** :
  - ✅ Performances excellentes
  - ✅ Concurrency native (500k+ records)
  - ✅ Typage fort, compilation
  - ✅ Petit binaire, déploiement simple
  - ✅ Ton expertise
- **Architecture** : handlers → services → repositories (clean)

#### Option 2 : Node.js/TypeScript
- **Framework** : Express, Fastify, ou NestJS
- **Avantages** :
  - ✅ Même langage frontend/backend (TypeScript)
  - ✅ Écosystème npm riche
  - ✅ Partage types entre front/back
- **Inconvénients** :
  - ⚠️ Performances moindres que Go pour haute charge

#### Option 3 : Maintenir Python ETL + ajouter layer
- **Avantages** :
  - ✅ Réutilisation logique existante
  - ✅ Moins de réécriture
- **Inconvénients** :
  - ⚠️ Dette technique perpétuée
  - ⚠️ SPOF non résolu

**Recommandation** : **Go** pour API layer nouvelle, maintenir Python ETL si logique métier complexe dedans, sinon remplacer.

### Base de données

**ERP Ogasys** : existant, pas de changement

**Cache** :
- **Redis** : sessions, cache requêtes fréquentes, rate limiting
- **Alternative** : Memcached (plus simple, moins features)

**Recherche** (si nécessaire) :
- **Meilisearch** : typo-tolerant, rapide, open-source
- **Alternative** : Algolia (SaaS, payant)

### DevOps & Infrastructure

**CI/CD** :
- **GitLab CI** (si Midbec utilise GitLab)
- **GitHub Actions** (si GitHub)
- **Alternative** : CircleCI, Jenkins

**Hosting** :
- **Frontend** : Vercel, Netlify, Cloudflare Pages
- **Backend** : Railway, Render, Fly.io, ou VPS classique

**Monitoring** :
- **Sentry** : tracking erreurs frontend/backend
- **Grafana + Prometheus** : métriques infrastructure
- **Alternative** : Datadog (all-in-one, payant)

**Logs** :
- **Loki** + Grafana : centralisation logs
- **Alternative** : ELK stack, CloudWatch

### Sécurité

**Auth** :
- À définir selon besoins (JWT? Sessions? OAuth?)

**SSH** :
- **Migration** : clés ED25519, désactivation password auth

**Secrets** :
- **HashiCorp Vault** ou **Doppler** ou **env variables** sécurisées

---

## 🔗 Comparaison avant/après

| Aspect | Legacy (PHP 5.6) | Moderne (React + Go/Node) |
|--------|------------------|---------------------------|
| **Sécurité** | ❌ EOL, vulnérable | ✅ Stack supportée, patchée |
| **Performance** | ⚠️ Limitée | ✅ Optimisée (cache, pagination) |
| **Scalabilité** | ❌ 500k+ = problèmes | ✅ Architecturé pour scale |
| **Maintenabilité** | ❌ Code legacy opaque | ✅ Clean code, tests, docs |
| **Dev experience** | ❌ CLI, pas d'env dev | ✅ Moderne (HMR, TypeScript, etc.) |
| **Déploiement** | ❌ Direct prod | ✅ CI/CD, staging, rollback |
| **Monitoring** | ❌ Inexistant | ✅ Metrics, logs, alertes |

---

## 📝 Décisions à prendre

### Court terme (avant démarrage officiel)
- [ ] **Hosting frontend** : Vercel vs Netlify vs autre ?
- [ ] **Backend choice** : Go vs Node.js vs hybride ?
- [ ] **SSR nécessaire** : Next.js vs Vite ?
- [ ] **Auth strategy** : JWT vs sessions vs OAuth ?

### Moyen terme (phase 1-2)
- [ ] **Framework UI** : shadcn vs MUI vs custom ?
- [ ] **State management** : Zustand vs Jotai vs Context ?
- [ ] **Testing** : Vitest + Playwright vs Jest + Cypress ?
- [ ] **Cache layer** : Redis obligatoire ou optionnel ?

### Long terme (phase 3+)
- [ ] **Remplacement ETL Python** : oui/non ? Si oui, quand ?
- [ ] **Redondance Ogasys** : failover possible ?
- [ ] **Observability complète** : Grafana stack vs Datadog ?

---

## 🔗 Liens connexes

- [[infrastructure-audit]] - État initial infrastructure
- [[migration-react]] - Détails projet migration (à créer)
- [[mission-overview]] - Contexte global mission

---

**Notes** : Stack cible à valider avec Patrick (admin sys) et business pour alignement budget/compétences.