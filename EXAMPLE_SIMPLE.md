
Refactor component app.component.ts:

```typescript
import { Component } from '@angular/core';
import { HorizonService } from './horizon.service';

@Component({
    selector: 'app-root',
    template: `
        <h1>{{title}}</h1>
        <form (submit)="add(todo)">
            <input type="text" [(ngModel)]="todo" name="todo">
            <button type="submit">Add</button>
        </form>
        <ul>
            <li *ngFor="let item of items | async">
                {{item.text}}
            </li>
        </ul>
    `
})
export class AppComponent {

    title = 'app works!';    
    todo: string = '';
    items: any;
    table = this.horizon.table('todos');

    constructor(private horizon: HorizonService) {
    }

    ngOnInit() {

        this.load();
    }

    load() {

        this.items = this.table
            .order('datetime', 'descending')
            .limit(10)
            .watch();
    }

    add(todo: string) {

        this.table.store({
            text: todo,
            datetime: new Date(),
        })

        // clear
        this.todo = '';
    }
}
```