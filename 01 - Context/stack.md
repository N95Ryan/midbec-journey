# 🛠️ Stack technique Midbec

---

## 🖥️ Frontend


| Technologie          | Version | Rôle                      |
| -------------------- | ------- | ------------------------- |
| Next.js (App Router) | 15.1.7  | Framework principal       |
| React                | 19      | UI                        |
| TypeScript           | 5.8     | Typage strict             |
| Tailwind CSS         | v4      | Styles                    |
| TanStack Query       | v5      | Server state              |
| Zustand              | v5      | Client state global       |
| react-intl           | —       | i18n FR/EN                |
| Bun                  | —       | Package manager & runtime |


---

## ⚙️ Backend


| Technologie | Rôle                                        |
| ----------- | ------------------------------------------- |
| Go + Chi    | API layer — handlers → services → repositories |
| PostgreSQL  | Base de données                             |
| UnoPIM      | Source de vérité produit (géré par Patrick) |


**Architecture Go :** handlers → services → repositories

---

## 🔌 Intégrations externes


| Système    | Rôle                                      | Accès              |
| ---------- | ----------------------------------------- | ------------------ |
| ERP Ogasys | Inventaire — catalogue pièces             | Lecture via Go API |
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

