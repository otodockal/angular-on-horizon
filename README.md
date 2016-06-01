
Angular on Horizon
==================

Run Angular 2 on Horizon.io in 5 steps.

PREREQUISITES
-------------
- Node.js 4+
- Angular CLI 
    - https://github.com/angular/angular-cli
    - npm install -g angular-cli
- Horizon.io CLI
    - http://horizon.io/install/
    - npm install -g horizon

STEPS
-----
[1] Open terminal

```bash 
ng new angular_on_horizon && cd angular_on_horizon && hz init
```

[2] Add horizon.js into index.html
    
```bash
open -t src/index.html 
# add `<script src="http://127.0.0.1:8181/horizon/horizon.js"></script>` under main app component
```

[3] Create Horizon service
    
```bash
ng g service horizon
open -t src/app/horizon.service.ts
# add `table = Horizon({host: 'localhost:8181'});` 
open -t src/typings.d.ts
# add `declare var Horizon: any;`
```

[4] Inject Horizon service

```bash
open -t src/main.ts
# replace `bootstrap(AngularOnHorizonAppComponent);`
# by
# `import {HorizonService} from './app/horizon.service'; bootstrap(AngularOnHorizonAppComponent, [HorizonService]);`
```

Horizon service can be used now everywhere in your component tree!

[5] run

```bash
hz serve --dev & ng serve & open http://localhost:4200
```