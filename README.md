# API Documentation

## List of available animals

These are the several animal strings that can be used to send a request to the API.

* `cat`
* `dog` 
* `bird` 
* `panda` 
* `redpanda` 
* `koala` 
* `fox` 
* `whale` 
* `kangaroo` 
* `bunny`

## Random image

```
https://api.animality.xyz/img/<animal>
```
This endpoint allows you to request a random image URL for a specific animal. The data returned is a JSON object with a URL to the specified image.
```json
{
  "link": "https://api.animality.xyz/img/dog/24.jpeg"
}
```

## Random fact

```
https://api.animality.xyz/fact/<animal>
```
This endpoint allows you to request a random fact for a specific animal. The data returned is a JSON object with the fact as a string.
```json
{
  "fact": "Spaying or neutering your dog can help prevent certain types of cancer."
}
```

# Official Wrappers
Here are some official wrappers for this API. If you can't find your programming language here, you can make your own.

## Node.js
```js
$ npm install animality
```
The node.js wrapper for this API is available for use in [Node Package Manager](https://www.npmjs.com/package/animality). It's use is pretty straight-forward.
```js
const animality = require('animality');
const animal = 'cat';
animality.getAsync(animal).then(console.log);
```
This outputs the following object in the terminal:
```json
{
  name: 'cat',
  image: 'An image URL here',
  fact: 'A fact here'
}
```
Other than that, this package also allows you to request multiple animals at the same time.
```js
const animality = require('animality');
const animals = ['cat', 'dog', 'panda'];
animality.getAsync(animals).then(console.log);
```
This outputs the following array of objects in the terminal:
```json
[
  {
    name: 'cat',
    image: 'An image URL here',
    fact: 'A fact here'
  },
  {
    name: 'dog',
    image: 'An image URL here',
    fact: 'A fact here'
  },
  {
    name: 'panda',
    image: 'An image URL here',
    fact: 'A fact here'
  }
]
```
## Python
```py
$ pip install animality-py
```
This API has a wrapper for it in Python. You can install it through the [Python Package Index](https://www.npmjs.com/package/animality). Using it is quite simple.
```py
import animality
from asyncio import get_event_loop

async def run():
    animal = await animality.get_animal("dog")
    print(animal)
    random = await animality.random()
    print(random)

    await animality.close()

get_event_loop().run_until_complete(run())
```
This outputs the following text in the terminal:
```js
<Animal name="dog" image="..." fact="...">
<Animal name="..." image="..." fact="...">
```
