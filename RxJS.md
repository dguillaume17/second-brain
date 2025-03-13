---
tags:
  - "#rxjs/switch-map"
  - "#rxjs/concat-map"
aliases:
  - Analyse de l'ordre d'exécution avec mergeMap et concatMap en RxJS
  - Comparaison des opérateurs RxJS mergeMap et concatMap"
---


```typescript
import { Subject, of } from 'rxjs';
import { delay, mergeMap, tap } from 'rxjs/operators';

const source = new Subject<void>();

const delay$ = of(null).pipe(
  tap(() => console.log('delay begins')),
  delay(1000),
  tap(() => console.log('delay ends'))
);

source.pipe(mergeMap(() => delay$)).subscribe();

source.next();
source.next();
source.next();
```

```console
delay begins
delay begins
delay begins
delay ends
delay ends
delay ends
```

```typescript
import { Subject, of } from 'rxjs';
import { concatMap, delay, tap } from 'rxjs/operators';

const source = new Subject<void>();

const delay$ = of(null).pipe(
  tap(() => console.log('delay begins')),
  delay(1000),
  tap(() => console.log('delay ends'))
);

source.pipe(concatMap(() => delay$)).subscribe();

source.next();
source.next();
source.next();
```

```console
delay begins
delay ends
delay begins
delay ends
delay begins
delay ends
```