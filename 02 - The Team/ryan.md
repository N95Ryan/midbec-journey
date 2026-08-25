# 👤 Ryan — Software Engineer (Solo Developer)

**Rôle** : Couche applicative fullstack — seul développeur sur le chantier de modernisation.

## Périmètre

- Architecture, choix techniques, implémentation et maintenance de l'app
- Frontend Next.js : UI/UX, composants, responsive, perf, SEO, accessibilité
- API Go (Chi) : auth, catalogue, checkout, commandes, factures, intégrations ERP / PartSmart / UnoPIM
- Migration progressive (strangler fig) sans interruption de service
- Qualité : tests, documentation, scopes livrables un commit à la fois

## Collaboration avec Patrick

Décisions techniques conjointes. Ryan porte le code ; Patrick porte l'infra, les accès sensibles et les pipelines de déploiement.

| Aspect | Patrick | Ryan |
|---|---|---|
| Périmètre | Infra, sécurité, ops, UnoPIM côté serveur | App, intégrations, UX |
| Environnements | Provisionnement dev / staging / prod | Consommation et feedback terrain |
| Bloquants typiques | OAuth PIM, import catalogue, accès ERP prod | Déblocage app dès que l'infra suit |

---

**Liens** : [mission.md](../01%20-%20Context/mission.md) · [stack.md](../01%20-%20Context/stack.md) · [patrick.md](./patrick.md)
