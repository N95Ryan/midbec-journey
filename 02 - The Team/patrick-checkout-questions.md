# Questions checkout ERP — pour Patrick

> Brouillon du 13 juillet 2026. Source détaillée : [`midbec-go-api/docs/erp-map.md`](../../midbec-go-api/docs/erp-map.md).

Salut Patrick,

Le proxy checkout est codé (`POST /api/orders`, `POST /api/orders/calculate`, bouton Commander branché). J’ai besoin de ton aide sur quatre points avant de valider en prod.

---

## 1. Annulation des commandes test (priorité haute)

Des commandes ont été créées pendant le spike du 9 juillet sur l’env test :

| order_no   | Contexte                    |
|------------|-----------------------------|
| `01W100903` | Spike create               |
| `01W100904` | Spike preview/create       |
| Autres ?   | Postman / `PROBE_ALLOW_CREATE` le 9 |

Peux-tu les annuler côté ERP test ? Je n’en créerai plus sans ton accord (`POST /orders` = auto-commit).

---

## 2. Totaux à 0 $ sur calculate / preview

**Fait établi :** `returncode=0` mais `sub_total` et `total` à **0.0** sur preview/calculate pour le SKU `80040`, alors que la grille B2B affiche retail ~3.47 $ / client ~2.16 $ hors flux commande.

**Questions :**
- Où lire le montant réel dans la réponse ERP (lignes `items`, autre nesting) ?
- Est-ce un comportement normal de l’env test ou un champ manquant dans notre POST ?

**Décision actuelle :** on garde les totaux panier **locaux** (Redux) à l’écran — on ne substitue pas par les totaux ERP tant qu’ils sont à 0.

---

## 3. Auto-commit vs preview pour le site

| Endpoint              | Comportement                          |
|-----------------------|---------------------------------------|
| `POST /orders`        | Auto-commit — commande réelle         |
| `POST /orders/preview`| Preview + `trans_id` (non commitée)   |
| `POST /orders/calculate` | Calcul seulement, pas de persist |

**Question :** pour midbec.ca, on doit utiliser quel flux ? Preview + `PUT /orders/commit/{trans_id}` ou create direct ?

---

## 4. Latence ERP (env test vs prod)

Mesures du 9 juillet sur `http://10.10.10.201:8088/test` :

| Endpoint                         | Moyenne |
|----------------------------------|---------|
| `GET /accounts/code/001020`      | ~12 s   |
| `GET /webusers?idwebuser=…`      | ~13 s   |
| `GET /orders/webuser/…`          | ~13 s   |

On a monté `ERP_TIMEOUT_SECONDS` à **30 s** en local test uniquement.

**Question :** cette latence est-elle spécifique à l’env test, ou représentative de la prod ? Ça détermine si on ajuste un timeout ou si on design un checkout async (loading 30–60 s, feedback utilisateur).

---

## Bonus (non bloquant)

- Legacy login : l’ERP peut-il résoudre `1020` nativement sur `/webusers` ?
- Email canonique : `patrick.ogrady@gmail.com` vs `pogrady@midbec.com` ?

Merci — dis-moi quand tu as 15 min pour le point checkout.
