# crm-react-table (GoDaddy CRM)

> [!IMPORTANT]
> **`main` holds no source code.** The `crm-react-table` package used by the CRM fleet is built and published from the **`v6-stable`** branch.

## Where the published package comes from

| Branch | `package.json` | Published to |
| --- | --- | --- |
| [`v6-stable`](https://github.com/gdcorp-crm/crm-react-table/tree/v6-stable) | `crm-react-table@6.10.4`, the version the fleet consumes | Artifactory `node-crm-local` |
| [`v6`](https://github.com/gdcorp-crm/crm-react-table/tree/v6) | `crm-react-table@6.11.6` | Artifactory `node-crm-local` |

To change the package the fleet uses, branch from `v6-stable` and open your PR against it, not against `main`.

### Build tooling on `v6-stable` needs modernizing before the next release

The published package has one runtime dependency, `classnames`. React, react-dom and prop-types are peer dependencies that consumers provide. None of the tooling below ships to consumers.

The branch's **build tooling**, however, dates from 2017–2018: babel 6, eslint 4, rollup 0.55, standard 10 and postcss-cli 2. As of 2026-09, `yarn audit` on its `yarn.lock` reports 12 critical and 58 high unique advisories, all reached through devDependencies.

Before publishing another v6 release, move the toolchain to current majors (babel 7, a current rollup and eslint), then refresh the lockfile.

## Upstream TanStack Table v8 source and examples

`main` previously mirrored upstream [TanStack Table v8](https://github.com/tanstack/table) (the `@tanstack/*` packages, docs, and examples). CRM never published it. It targets the v8 API, not the v6 API the fleet uses. It is preserved in git history at [`9b0a307`](https://github.com/gdcorp-crm/crm-react-table/tree/9b0a307e4e2101d2cc5bbbefc01a1827cee42ac1):

- [Browse `examples/` at that commit](https://github.com/gdcorp-crm/crm-react-table/tree/9b0a307e4e2101d2cc5bbbefc01a1827cee42ac1/examples)
- [Commit history of `examples/`](https://github.com/gdcorp-crm/crm-react-table/commits/9b0a307e4e2101d2cc5bbbefc01a1827cee42ac1/examples)
- [Upstream v8 README at that commit](https://github.com/gdcorp-crm/crm-react-table/blob/9b0a307e4e2101d2cc5bbbefc01a1827cee42ac1/README.md)

## Where it is used in the fleet

Consumers install it under the `react-table` alias from [crmjs-ui](https://github.com/gdcorp-crm/crmjs-ui) (`"react-table": "npm:crm-react-table@6.10.4"` in [`package.json`](https://github.com/gdcorp-crm/crmjs-ui/blob/HEAD/package.json)). The shared wrapper is [`crmjs-ui/src/crm-react-table/v2`](https://github.com/gdcorp-crm/crmjs-ui/tree/HEAD/src/crm-react-table/v2) (`CrmReactTable`, pagination, loading states). These working usages are the best examples for the v6 API:

- crmjs-ui: [`src/entitlements/constants.js`](https://github.com/gdcorp-crm/crmjs-ui/blob/HEAD/src/entitlements/constants.js), [`src/associated-bills/constants.js`](https://github.com/gdcorp-crm/crmjs-ui/blob/HEAD/src/associated-bills/constants.js)
- [crm-ui-lib-orders](https://github.com/gdcorp-crm/crm-ui-lib-orders/blob/HEAD/src/orders/constants.js): `src/orders/constants.js`
- [crm-ui-lib-launch-pad](https://github.com/gdcorp-crm/crm-ui-lib-launch-pad/blob/HEAD/src/launch-pad/agents/constants.js): `src/launch-pad/agents/constants.js`
- [crm-ui-lib-customer-search](https://github.com/gdcorp-crm/crm-ui-lib-customer-search/blob/HEAD/src/customer-search/search-results/constants.js): `src/customer-search/search-results/constants.js`
- [crm-ui-lib-messages](https://github.com/gdcorp-crm/crm-ui-lib-messages/blob/HEAD/src/messages/messages-table/constants.js): `src/messages/messages-table/constants.js`
- [crm-ui-lib-contact-info](https://github.com/gdcorp-crm/crm-ui-lib-contact-info/blob/HEAD/src/contact-info/change-history/constants.js): `src/contact-info/change-history/constants.js`
- [crm-ui-lib-payments](https://github.com/gdcorp-crm/crm-ui-lib-payments/blob/HEAD/src/crm-ui-lib-payments/payments-table/constants.js): `src/crm-ui-lib-payments/payments-table/constants.js`
- [crm-ui-lib-customer-home](https://github.com/gdcorp-crm/crm-ui-lib-customer-home/blob/HEAD/src/customer-home/orders/components/OrdersTable.jsx): `src/customer-home/orders/components/OrdersTable.jsx`

## License

MIT. See [LICENSE](LICENSE); the original code is © Tanner Linsley.
