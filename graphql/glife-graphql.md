# Glife Technologies GraphQL API

GraphQL API backing the [Glife](https://glife.com.sg) food-tech commerce and supply-chain platform.

- Endpoint: `https://api-sg.glifeware.com/graphql`
- Transport: single HTTP POST endpoint (Apollo Server); GraphQL subscriptions for realtime
- Auth: bearer token from the `login` / `loginEcommerce` mutations (see `../authentication/glife-authentication.yml`)

> Captured by the API Evangelist enrichment pipeline via live GraphQL introspection on 2026-07-19.
> This is Glife's application backend; it is publicly reachable with introspection enabled but is not a formally published/developer-documented API.

## Schema file

See [`glife-schema.graphql`](./glife-schema.graphql) for the full SDL, and
[`glife-graphql-introspection.json`](./glife-graphql-introspection.json) for the raw introspection response.

## Surface

| Root | Fields |
|------|--------|
| Query | 535 |
| Mutation | 870 |
| Subscription | 139 |

## Type inventory

| Kind | Count |
|------|-------|
| Object | 729 |
| Input object | 282 |
| Enum | 235 |
| Scalar (custom) | 8 |

Custom scalars: `String`, `Float`, `Boolean`, `Int`, `Date`, `JSON`, `JSONObject`, `BigInt`

## Domains

The schema spans Glife's full operation:

- **Ecommerce** — customers, addresses, products, categories, orders, articles/content, promotions
- **Supply chain** — purchase/sales orders, invoices, vendors, warehouses, inventory, goods receive/issue notes, standing orders, deliveries
- **Pricing** — contract/group/promotion pricing, currencies, payment terms
- **Operations** — teams, roles/permissions, vehicles, notifications, badges

## Conventions

- **Pagination** — offset style (`all<Entity>(page, perPage, sortField, sortOrder, filter)`) with a paired `_all<Entity>Meta { count }` count query (react-admin `ra-data-graphql` convention).
- **Realtime** — `<Entity>SubscriptionPayload { mutation, node, previousValues }` subscriptions.

See `../conventions/glife-conventions.yml` and `../data-model/glife-data-model.yml`.
