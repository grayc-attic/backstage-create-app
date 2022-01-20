# Development

## Prepare

Add guest login in ``:

```ts
  SignInPage: props => (
    <SignInPage
     {...props}
-    auto
-    provider={githubProvider}/>
+    providers={['guest', githubProvider]}/>
  ),
```

Get decrypted secrets from [backstage.env](https://github.com/grayc-de/flux-grayc-de/blob/main/backstage/secret/backstage.env).

## Run Backstage

```sh
cat backstage.env | grep '=' | sed 's/=/: /' > app-config.secret.yaml
cp app-config.dev.yaml app-config.local.yaml
yarn install
yarn dev
```
