# Maintenance

Update versions:

```sh
yarn backstage-cli versions:bump --pattern '@{backstage,roadiehq}/*'
yarn backstage-cli versions:check --fix
rm yarn.lock && yarn install && yarn tsc && yarn build
```

Track updates in example app:

```sh
npx @backstage/create-app --path . 
```

## Links

* backstage.io: [Keeping Backstage Updated](https://backstage.io/docs/getting-started/keeping-backstage-updated)
