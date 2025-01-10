# Class
```ts
interface ExampleInterface{
	foo: string;
	bar: number;
}

class Example implements ExampleInterface{
	foo: string;
	bar: number;

	constructor(init: ExampleInterface){
		this.foo = init.foo;
		this.bar = init.bar;
	}
}
```
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