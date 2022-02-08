# Development

## Prepare

Add guest login in [App.tsx](https://github.com/grayc-de/backstage/blob/docs/packages/app/src/App.tsx):

```ts
  SignInPage: props => (
    <SignInPage
     {...props}
-    auto
-    providers={[githubProvider, googleProvider]}/>
+    providers={[githubProvider, googleProvider, 'guest']}/>
  ),
```

## Run Backstage

Get decrypted secrets from [backstage.env](https://github.com/grayc-de/flux-grayc-de/blob/main/backstage/secret/backstage.env).

```sh
cat backstage.env | grep '=' | sed 's/=/: /' > app-config.secret.yaml
cp app-config.dev.yaml app-config.local.yaml
yarn install
yarn dev
```
