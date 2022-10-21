# Manually remove item from cache
```js
const mutationFunction = async()=>{
	try{
		const res = await mutateExample({
			variables:{
				//...mutation input
			},
			update(cache) {
				const normalizedId = cache.identify({
					id: <item>.id,
					__typename: 'ItemType'
				})

				cache.evict({ id: normalizedId });
				
				cache.gc();
			},
		});
	} catch(error) {
		console.error(error);
	}
}
```