# Deploy to Firebase

A GitHub Action to deploy to Firebase.

- Make sure that you checkout the repository using the [actions/checkout](https://github.com/actions/checkout) action
- Make sure that you have the `firebase.json` file in the repository
- To obtain the Firebase token, run `firebase login:ci` on your local computer and [store the token](https://docs.github.com/en/actions/reference/encrypted-secrets#creating-encrypted-secrets-for-a-repository) as the `FIREBASE_TOKEN` secret
- Specify the Firebase project name in the `FIREBASE_PROJECT` env var
- If you would like to deploy only hosting, set `FIREBASE_ONLY_HOSTING` to true
- To use a specific firebase environment, set `FIREBASE_ENVIRONMENT`

## Workflow examples

Deploy the `main` branch when a commit is pushed to it:

```
name: Deploy the main branch
on:
  push:
    branches:
      - main
jobs:
  main:
    name: Deploy to Firebase
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - uses: noalaltd/deploy-firebase@main
      env:
        FIREBASE_TOKEN: ${{ secrets.FIREBASE_TOKEN }}
        FIREBASE_PROJECT: name-of-the-project
```

Deploy only when a tag starts with `v` is pushed:

```
name: Deploy a tag
on:
  push:
    tags:
      - v*
jobs:
  main:
    name: Deploy to Firebase
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - uses: noalaltd/deploy-firebase@main
      env:
        FIREBASE_TOKEN: ${{ secrets.FIREBASE_TOKEN }}
        FIREBASE_PROJECT: name-of-the-project
        FIREBASE_ONLY_HOSTING: true
```
Deploy a specific environment configuration https://firebase.google.com/docs/functions/config-env#deploying_multiple_sets_of_environment_variables
```
name: Deploy the main branch
on:
  push:
    branches:
      - main
jobs:
  main:
    name: Deploy to Firebase
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - uses: noalaltd/deploy-firebase@main
      env:
        FIREBASE_TOKEN: ${{ secrets.FIREBASE_TOKEN }}
        FIREBASE_PROJECT: name-of-the-project
        FIREBASE_ENVIRONMENT: prod
```
