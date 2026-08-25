# 🛠️ Stack technique Midbec

---

## 🖥️ Frontend


| Technologie          | Version | Rôle                                      |
| -------------------- | ------- | ----------------------------------------- |
| Next.js (App Router) | 15.5.x  | Framework principal                       |
| React                | 19      | UI                                        |
| TypeScript           | 5.8     | Typage strict                             |
| Tailwind CSS         | v4      | Styles                                    |
| TanStack Query       | v5      | Server state                              |
| Redux Toolkit        | v2      | Client state global (migration Zustand prévue) |
| next-intl              | v4      | Routing & locale (`[locale]`, middleware) |
| react-intl           | v7      | Strings composants (coexistence transitoire) |
| react-hook-form      | v7      | Formulaires                               |
| lucide-react         | —       | Icônes                                    |
| Bun                  | —       | Package manager, runtime & tests (`bun test`) |


---

## ⚙️ Backend


| Technologie | Version | Rôle                                        |
| ----------- | ------- | ------------------------------------------- |
| Go          | 1.25.x  | Langage API                                 |
| Chi         | v5      | Router HTTP                                 |
| pgx         | v5      | Driver PostgreSQL                           |
| PostgreSQL  | —       | Base de données                             |
| UnoPIM      | —       | Source de vérité produit (géré par Patrick) |

**Architecture Go :** handlers → services → repositories

---

## 🔌 Intégrations externes


| Système    | Rôle                                      | Accès              |
| ---------- | ----------------------------------------- | ------------------ |
| ERP Ogasys | Inventaire, checkout, factures, comptes   | Lecture/écriture via Go API |
| PartSmart  | Catalogue modèles + IPL (LeadVenture)     | Via Go proxy       |
| Cloudflare | CDN / DNS                                 | Géré par Patrick   |


---

## 🏗️ Infra & DevOps

Périmètre Patrick — LXC containers, GitLab CI/CD.

---

## 📐 Principes d'architecture

- **UI First** : fake data → validation visuelle → branchement Go API
- **Strangler fig** : migration domaine par domaine, jamais tout d'un coup
- **KISS** : solution la plus simple qui répond au besoin
- **Un scope = un prompt = un commit**
