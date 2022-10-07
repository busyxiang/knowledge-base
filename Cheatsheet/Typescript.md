# Type Utility
### Array Element
Get array item type
```typescript
export type ArrayElement<T> = T extends (infer U)[] ? U : null;
```
