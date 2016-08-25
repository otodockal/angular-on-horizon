
Angular on Horizon
==================

Run [Angular 2](https://angular.io/) on [Horizon.io](https://horizon.io/) in 5 steps.  
This Cookbook is only about setting up Horiozon DEV server with Angular 2 the easiest way.  
Horizon.io is built on top of RxJS, so integration with Angular 2 is pretty seamless.  
Cookbook is macOS(OS X) only for now and WIP.

PREREQUISITES
-------------
- Node.js 4+
    - https://nodejs.org/en/download/
- Angular CLI
    - npm install -g angular-cli@webpack
    - https://github.com/angular/angular-cli/
- Horizon.io CLI
    - npm install -g horizon
    - http://horizon.io/install/

STEPS (macOS)
-------------
[1] Open terminal

```bash 
ng new angular_on_horizon && cd angular_on_horizon && hz init && npm install && npm install @horizon/client --save
```

[2] Create Horizon service
    
```bash
ng g service horizon
nano src/app/horizon.service.ts
```

```typescript
// replace file by:
import {Injectable} from '@angular/core';
var Horizon = require('@horizon/client');

@Injectable()
export class HorizonService {
    table = Horizon({host: 'localhost:8181'});
}
```


[3] Declare typings

NOTE: this step will not be needed soon! ◦°˚\(*❛‿❛)/˚°◦ (https://github.com/rethinkdb/horizon/pull/741)

```bash
nano src/typings.d.ts
```

```typescript
// add
declare var Horizon: any;
```


[4] Inject Horizon service

```bash
nano src/app/app.module.ts
```

```typescript
// add
import {HorizonService} from './horizon.service';
// replace providers
providers: [HorizonService],
```

Horizon service can be used now everywhere in your component tree!

[5] run

```bash
hz serve --dev & ng serve & open http://localhost:4200
```