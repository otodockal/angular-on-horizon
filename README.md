
Angular on Horizon
==================

Run [Angular 2](https://angular.io/) on [Horizon.io](https://horizon.io/) in 5 steps.
This Cookbook is only about setting up Horiozon DEV server with Angular 2 the easiest way.  
Horizon.io is built on top of RxJS, so integration with Angular 2 is pretty seamless.  
Cookbook is macOS(OS X) only for now and WIP.

## PREREQUISITES
- Node.js 4+
    - https://nodejs.org/en/download/
- TypeScript 2.1
    - http://www.typescriptlang.org/
- Angular CLI
    - npm install -g angular-cli@webpack
    - https://github.com/angular/angular-cli/
- Horizon.io CLI
    - npm install -g horizon
    - http://horizon.io/install/

## Table of Contents
- [macOS (OSX)](#macos-osx)
- [Windows](#windows)

## macOS (OSX)
### 1. Open terminal

```bash 
ng new AngularOnHorizon && cd AngularOnHorizon && hz init && npm install && npm install @horizon/client --save
```

### 2. Create Horizon service
    
```bash
ng g service horizon
nano src/app/horizon.service.ts
```

```typescript
// replace file by:
import {Injectable} from '@angular/core';
const Horizon = require('@horizon/client');

@Injectable()
export class HorizonService {
    table = Horizon({host: 'localhost:8181'});
}
```

### 3. Inject Horizon service

```bash
nano src/app/app.module.ts
```

```typescript
// add
import { HorizonService } from './horizon.service';
// replace providers
providers: [HorizonService],
```

Horizon service can be used now everywhere in your component tree!

### 4. Run Horizon (dedicated terminal)

```bash
hz serve --dev
```

### 5. Run Angular app (dedicated terminal)

```bash
ng serve & open http://localhost:4200
```

## Windows

PR more than welcome!

## EXAMPLE
Refactor [app.component.ts](EXAMPLE_SIMPLE.md)