# 🗂️ Tech Notes Draft

> Notes techniques extraites des daily logs. À trier et déplacer dans les notes de projet dédiées.

---

## 🔧 Template RedParts — Architecture

### Pattern injectable

```
api/
├── base/          Classes abstraites (contrats)
└── fake-api/      Implémentations fake
```

Passer à backend Chi → créer une nouvelle implémentation des classes abstraites, changer les exports dans `api/index.ts`. **Zéro impact sur l'UI.**

### État du template (Jour 1)

- ~75 pages Next.js déjà construites (catalogue, produit, panier, checkout, compte)
- Système SCSS custom : 212 fichiers, 9 sections, thèmes multiples (`$theme-color: #e52727`)
- Redux : 9 slices (cart, wishlist, compare, shop, user, currency, quickview, mobileMenu, options, garage)
- i18n avec react-intl (FR/EN ready)

### Système "Garage" à supprimer

- Interface `IVehicle { year, make, model, engine }` → remplacer par `IAppliance { brand, type, model, serialNumber }`
- Slice Redux `garage` (6 fichiers)
- Composants : `VehicleSelect`, `VehicleForm`, `VehiclePickerModal`
- Page `/account/garage`
- Bloc hero Home `BlockFinder`
- Filtres catalogue par véhicule
- Badge compatibilité pièce/véhicule
- Pages `/demo/*` (~40 pages à nettoyer)

### Cartographie terminologie

| Avant (auto) | Après (électroménager) |
|---|---|
| `vehicle` | `appliance` |
| `make` | `brand` |
| `partNumber` | `referenceNumber` |
| `compatibility` (IDs véhicules) | compatibilité modèle appareil |
| Catégories auto | Catégories électroménager |

---

## 🐛 Bug Go/Chi — `GET /api/me` → 401 Unauthorized

**Cause** : Collision de context key entre deux packages

```go
// authctx.go  → ctx.WithValue(r.Context(), contextKey(1), user)
// reqctx.go   → r.Context().Value(contextKey(0))
// → clés différentes → contexte jamais trouvé → 401
```

**Fix** : Centraliser la définition de la clé dans un seul package (`reqctx`) et l'importer dans `authctx.go`.

**Statut** : Identifié le 10 mars — pas encore appliqué.

---

## 📦 Migration stack front — Détail versions

| Dépendance | Avant | Après |
|---|---|---|
| Next.js | 11 | 15.1.7 |
| React | 17 | 19.0.0 |
| TypeScript | 4 | 5.8.2 |
| Tailwind CSS | — | v4 |
| Zustand | — | v5 |
| TanStack Query | — | v5 |

**Décisions :**
- Next.js 15.2.x écarté : régression Pages Router confirmée → 15.1.7 retenu, à surveiller dans les changelogs
- `next-redux-wrapper` supprimé : incompatible Next.js 15 → Redux natif
- `redux-devtools-extension` remplacé par `@redux-devtools/extension`
- `full-icu` supprimé : obsolète depuis Node.js 13
- Redux / Bootstrap / Sass conservés temporairement → migration = session dédiée

---

## 🔬 Outils à évaluer

### Go Micro
https://github.com/micro/go-micro

Framework Go pour systèmes distribués et microservices. Couche d'abstraction sur les problèmes classiques d'architectures distribuées. À évaluer vs Gin/Echo classique pour le backend Midbec.

### UnoPIM
https://unopim.com/

PIM open-source basé sur Laravel, API REST ou GraphQL intégrée. Pourrait gérer les 500k+ pièces avec leurs références, compatibilités, images. Question ouverte : UnoPIM + couche Go custom vs backend Go pur ?

---

## 🏗️ Décisions architecture (tableau de bord)

| Question | Décision |
|---|---|
| Redux → Zustand ? | Oui, mais **phase dédiée** |
| SCSS → Tailwind ? | Migration progressive |
| Next.js 11 → upgrade ? | Fait (15.1.7) |
| API fake → Chi ? | Conserver fake pendant dev front |
| `IVehicle` → `IAppliance` ? | Oui : `{ brand, type, model, serialNumber }` |
| Go Micro vs Chi ? | À évaluer avec Patrick |
| UnoPIM pertinent ? | À évaluer |
