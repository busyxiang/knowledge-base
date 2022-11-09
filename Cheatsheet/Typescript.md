# Generic
```ts
class Example<T>{
	item: T;

	constructor(item: T){
		this.item = item;
	}
}
```
## Optional
```ts
class Example<T = {}>{
	item: T;

	constructor(item: T){
		this.item = item;
	}
}
```
# Type Utility
### Array Element
Get array item type
```typescript
export type ArrayElement<T> = T extends (infer U)[] ? U : null;
```
