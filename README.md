# Vue Films

Projet développé il y a deux ans dans le cadre d'une initiation à Vue.js

URL production : [https://lockev-devops-docker.herokuapp.com/#/](https://lockev-devops-docker.herokuapp.com/#/)

URL pré-production : [https://lockev-devops-docker-preprod.herokuapp.com/#/](https://lockev-devops-docker-preprod.herokuapp.com/#/)

## Fonctionnement des workflows

L'approche CI/CD permet d'augmenter la fréquence de distribution des applications grâce à l'introduction de l'automatisation au niveau des étapes de développement des applications. Les principaux concepts liés à l'approche CI/CD sont l'intégration continue, la distribution continue et le déploiement continu.

Cette approche est interprété par github actions via les fichiers .yml dans [.github/workflows](https://github.com/IIM-Creative-Technology/devops-docker-guillaume-prigent/tree/master/.github/workflows)

Les fichiers deploy et deploy_preprod sont identiques, ils s'exécutent respectivement lors de commit sur les branches master et develop. Le fichier pr.yml est quant à lui appelé lorsqu'une pull request est effectuée sur le repository.

Lorsque qu'un fichier de workflow est appelé par la condition "on:" , il exécutera ses "jobs:". Chaque job est constitué de "steps", qui s'exécuteront dans l'ordre si l'étape précédente s'est complétée avec succès.

### Etapes présentes dans tous les fichiers .github/workflows

Initialisation du repository git
```
 - name: "Init repository"
   uses: actions/checkout@v2
```

Précisons que la version du node employée par le projet est 14.x.x
```
 - name: "Setup Node"
   uses: actions/setup-node@v2
   with:
     node-version: '14'
```

Initialisation des dépendances node
```
 - name: "Install dependencies"
   run: npm install
```

Initialisation d'un linter (eslint)
```
 - name: "Run linter"
   uses: stefanoeb/eslint-action@1.0.2
```

Lancement des tests unitaires
```
 - name: "Run tests"
   run: npm run test:unit
```

### Uniquement dans deploy.yml et deploy_preprod.yml

Lancer l'application en mode production (build)
```
- name: "Build app"
  run: npm run build
```

Installer Ruby afin de déployer sur Heroku
```
- name : "Install ruby"
  uses: ruby/setup-ruby@v1
  with:
    ruby-version: 2.7

- name : "Install DPL"
  run: gem install dpl

- name: "Deploy to Heroku"
  run: dpl --provider=heroku --app=${{secrets.HEROKU_APP}} --api-key=${{secrets.HEROKU_API_KEY}  --skip_cleanup=true
```

## Project setup

```
npm install
```

### Compiles and hot-reloads for development

```
npm run serve
```

### Compiles and minifies for production

```
npm run build
```

### Lints and fixes files

```
npm run lint
```

### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).

