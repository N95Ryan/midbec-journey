# Checklist spot-check B2B — navigateur

> À exécuter avec API Go (`:8080`) + front Next.js (`:3000`) et accès ERP (VPN/bureau si nécessaire).
> Complète la validation API du [7 juillet](../03%20-%20Daily%20logs/07%20-%20Juillet%202026/2026-07-07.md).

## Prérequis

```bash
# Terminal 1
cd ~/Desktop/DEV/midbec/midbec-go-api && go run ./cmd/main.go

# Terminal 2
cd ~/Desktop/DEV/midbec/midbec-front && npm run dev
```

Compte test avec `priceProfile` (ex. P2ELECTRO) — **ne pas confondre** les comptes sans rattachement client.

## Checklist

| # | Zone | Anonyme | Connecté B2B | OK ? |
|---|------|---------|--------------|------|
| 1 | Fiche produit SKU `80040` — prix affiché | retail ~3.47 $ | cust ~2.16 $ | ☐ |
| 2 | Prix barré (compareAt) si discount | — | visible si cust < retail | ☐ |
| 3 | Recherche header mode pièce | retail | cust si session | ☐ |
| 4 | Page `/recherche?q=80040` | retail | cust si session | ☐ |
| 5 | Listing catégorie (carte produit) | retail | cust si session | ☐ |
| 6 | Session `mb_session` conservée après F5 | — | toujours connecté | ☐ |
| 7 | Panier — totaux locaux (shipping/tax) | cohérents | cohérents | ☐ |

## Tests automatisés (unitaires)

```bash
cd ~/Desktop/DEV/midbec/midbec-front
bun test src/lib/api/pim.types.test.ts src/lib/catalog/isProductOrderable.test.ts
```

## Smoke API (sans navigateur)

```bash
cd ~/Desktop/DEV/midbec/midbec-go-api
./scripts/b2b-pricing-smoke.sh
```

## Notes du 13 juillet

- Tests unitaires `getDisplayPrice` / `getProductPriceFields` : logique B2B validée en code.
- Spot-check navigateur : **en attente** accès VPN/bureau + serveurs locaux démarrés manuellement.
