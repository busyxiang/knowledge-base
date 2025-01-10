# Hooks
## useState
### Initialize state with function
```js
const [state, setState] = useState(()=>{
	//...rest
});
```
# Generic
```jsx
const Component = <T,>(props: Props<T>)=>{
	// ...component codes
}
```
# Check text overflow state
```jsx
const OverflowText = ()=>{
	const divRef = useRef(null);

	const isEllpisisActive = ()=>{
		if(!divRef.current) return false;

		return (
			divRef.currrent.offsetHeight < divRef.current.scrollHeight ||
			divRef.current.offsetWidth < divRef.current.scrollWidth
		);
	}

	return (
		<div
			ref={divRef}
			style={{
				overflow: 'hidden',
				textOverflow: 'ellipsis',
				whiteSpace: 'nowrap'
			}}
		>
			Super long long long long long long long long long long title
		</div>
	)
}
```
---