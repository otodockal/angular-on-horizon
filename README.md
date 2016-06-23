
Angular on Horizon
==================

Run [Angular 2](https://angular.io/) on [Horizon.io](https://horizon.io/) in 5 steps.  
This Cookbook is only about setting up Horiozon DEV server with Angular 2 the easiest way.  
Horizon.io is built on top of RxJS, so integration with Angular 2 is pretty seamless.  
Cookbook is macOS(OS X) only for now.

PREREQUISITES
-------------
- Node.js 4+
    - https://nodejs.org/en/download/
- Angular CLI 
    - https://github.com/angular/angular-cli/
    - npm install -g angular-cli
- Horizon.io CLI
    - http://horizon.io/install/
    - npm install -g horizon

STEPS (macOS)
-------------
[1] Open terminal

```bash 
ng new angular_on_horizon && cd angular_on_horizon && hz init && npm install
```

[2] Add horizon.js into index.html
    
```bash
nano src/index.html 
# add `<script src="http://127.0.0.1:8181/horizon/horizon.js"></script>` under <app-root> component
```

[3] Create Horizon service
    
```bash
ng g service horizon
nano src/app/horizon.service.ts
# add `table = Horizon({host: 'localhost:8181'});` 
nano src/typings.d.ts
# add `declare var Horizon: any;` NOTE: temporarily (https://github.com/rethinkdb/horizon/pull/531)
```

[4] Inject Horizon service

```bash
nano src/main.ts
# replace `bootstrap(AppComponent);`
# by
# `import {HorizonService} from './app/horizon.service'; bootstrap(AppComponent, [HorizonService]);`
```

Horizon service can be used now everywhere in your component tree!

[5] run

```bash
hz serve --dev & ng serve & open http://localhost:4200
```