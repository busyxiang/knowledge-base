# Index
1. [Date](#Date)
2. [Number](#number)
# Object
## Deconstruct
```js
const data = {
	foo: 'foo',
	bar: {
		fooBar: 'foobar'
	},
	fooBar: ['foo', 'bar'],
}

const {
	foo, 
	bar: { fooBar }, 
	foorBar: [fooItem, barItem]
} = data;
```

# Date
```js
new Date().toLocaleString()
// => 24/4/2022, 10:40:00 am

console.log(new Date().toLocaleString('en-US'))
// => 4/24/2022, 10:40:00 AM
console.log(new Date().toLocaleString('en-GB'))
// => 24/04/2022, 10:40:00
console.log(new Date().toLocaleString('ko-KR'))
// => 2022. 4. 24. Ïò§Ï†Ñ 10:40:49

console.log(new Date().toLocaleString('en-US', {
    year: 'numeric',
    weekday: 'long',
    month: 'long',
    day: 'numeric',
    hour: 'numeric',
    minute: 'numeric',
    second: 'numeric',
    hour12: false,
}))
// => Sunday, April 24, 2022 at 10:40:00

console.log(new Date().toLocaleString('en-US', {
    dateStyle: 'full',
}))
// => Sunday, April 24, 2022

console.log(new Date().toLocaleString('en-US', {
    dateStyle: 'full',
    timeStyle: 'full',
}))
// => Sunday, April 24, 2022 at 10:40:00 AM India Standard Time

console.log(new Date().toLocaleString('en-US', {
    calendar: 'indian',
}))
// => 2/4/1944 Saka, 10:40:00 AM
// I don't know what that means either

console.log(new Date().toLocaleString('en-US', {
    dayPeriod: 'long',
}))
// => in the morning

console.log(new Date().toLocaleString('en-US', {
    era: 'long',
    dayPeriod: 'long',
    weekday: 'long',
    month: 'long',
    year: 'numeric',
    day: '2-digit',
    hour: '2-digit',
    minute: '2-digit',
    second: '2-digit',
    fractionalSecondDigits: 3,
    timeZoneName: 'long',
}))
// => Sunday, April 24, 2022 Anno Domini at 10:00:00.124 in the morning India Standard Time
```
# Number
```js
console.log(10000000..toLocaleString())
// => 10,000,000

// currency
10000..toLocaleString('en-US', {style: 'currency', currency: 'USD'})
// => $10,000.00

10000..toLocaleString('en-US', {style: 'currency', currency: 'USD', currencyDisplay: 'name'})
// => 10,000.00 US dollars

(-11.29).toLocaleString('en-US', {style: 'currency', currency: 'USD', currencySign: 'accounting'})
// => ($11.29)

(-11.29).toLocaleString('en-US', {style: 'currency', currency: 'USD', currencySign: 'standard'})
// => -$11.29

// scientific
10000..toLocaleString('en-US', {notation: 'scientific'})
// => 1E4

10000..toLocaleString('en-US', {notation: 'compact'})
// => 10K
1234..toLocaleString('en-US', {notation: 'compact'})
// => 1.2K

1234..toLocaleString('en-US', {notation: 'engineering'})
// => 1.234E3

1234..toLocaleString('en-US', {notation: 'engineering', signDisplay: 'always'})
// => +1.234E3

0.55.toLocaleString('en-US', {style: 'percent'})
// => 55%

1234..toLocaleString('en-US', {style: 'unit', unit: 'liter'})
// => 1,234 L

1234..toLocaleString('en-US', {style: 'unit', unit: 'liter', unitDisplay: 'narrow'})
// => 1,234L
```
# Function
## Self Invoking
```js
(async ()=>{
	//...codes
})()
```
# JSON
## Pretty Print
```js
JSON.stringify(<input>, null, 2)
```