# animality-docs
The official API Documentation for animality

# Usage
These are the 18 animal strings that can be used to send a request to the API:
* `cat`
* `dog`
* `bird`
* `panda`
* `redpanda`
* `koala`
* `fox`
* `whale`
* `dolphin`
* `kangaroo`
* `bunny`
* `lion`
* `bear`
* `frog`
* `duck`
* `penguin`
* `axolotl`
* `capybara`

### [Random Image](https://api.animality.xyz/img/dog)
```
https://api.animality.xyz/img/<animal>
```

This endpoint allows you to request a random image URL for a specific animal. The data returned is a JSON object with a URL to the specified image.

```json
{
  "link": "https://api.animality.xyz/images/dog/15.png"
}
```

### [Random Fact](https://api.animality.xyz/fact/dog)
```
https://api.animality.xyz/fact/<animal>
```

This endpoint allows you to request a random fact for a specific animal. The data returned is a JSON object with the fact as a string.

```json
{
  "fact": "Dogs are as smart as a two-year-old baby."
}
```

# Official Wrappers
Here are some official wrappers for this API. If you can't find your programming language here, you can make your own.

## [Node.js](https://www.npmjs.com/package/animality)
### Installation
```bash
$ npm install animality
```

The Node.js wrapper for this API is available for use in [Node Package Manager](https://www.npmjs.com/package/animality). It's use is pretty straight-forward.

### Example
```js
const animality = require('animality');
const animal = 'cat';
animality.getAsync(animal, 'API_KEY').then(console.log);
```

This outputs the following object in the terminal:

```json
{
  "name": "cat",
  "image": "An image URL here",
  "fact": "A fact here"
}
```

Other than that, this package also allows you to request multiple animals at the same time.

```js
const animality = require('animality');
const animals = ['cat', 'dog', 'panda'];
animality.getAsync(animals, 'API_KEY').then(console.log);
```

This outputs the following array of objects in the terminal:

```json
[
  {
    "name": "cat",
    "image": "An image URL here",
    "fact": "A fact here"
  },
  {
    "name": "dog",
    "image": "An image URL here",
    "fact": "A fact here"
  },
  {
    "name": "panda",
    "image": "An image URL here",
    "fact": "A fact here"
  }
]
```

## [Python](https://pypi.org/project/animality-py)
### Installation
```bash
$ pip install animality-py
```

This API has a wrapper for it in Python. You can install it through the [Python Package Index](https://pypi.org/project/animality-py). Using it is quite simple.

### Example
```py
import animality
from asyncio import get_event_loop

async def run():
    animal = await animality.get("dog")
    print(animal.name, animal.image, animal.fact)
    random = await animality.random()
    print(random.name, random.image, random.fact)

get_event_loop().run_until_complete(run())
```

This outputs the following text in the terminal:

```js
<Animal name="dog" image="..." fact="...">
<Animal name="..." image="..." fact="...">
```

## [C/C++](https://github.com/animality-xyz/animality.h)
Required dependencies:
- [`libcurl`](https://github.com/curl/curl) (Linux only)
- `pthreads` (Linux only, might be already installed by default)
- `wininet` (Windows only, might be already installed by default)

### Installation
#### Windows (MinGW) or Linux
```sh
$ git clone https://github.com/animality-xyz/animality.h.git && cd animality.h/
$ gcc -c animality.c -o animality.o
$ ar rcs -o libanimal.a animality.o
```

#### Windows (Visual C++)
```bat
$ git clone https://github.com/animality-xyz/animality.h.git && cd animality.h
$ cl /LD animality.c
```

### Example
The response from requesting to the library is this struct.
```c
typedef struct {
    an_type_t type;    // animal name, as enum
    char * name;       // animal name, as string
    char * image_url;  // animal image URL
    char * fact;       // animal fact
} animal_t;
```

Here is a simple request example to the API. Please note that the following example is synchronous (aka blocking).

```c
#include "animality.h"

int main() {
    // create our animal struct
    animal_t animal = AN_EMPTY_ANIMAL;

    // request for an animal
    an_get(AN_DOG, &animal);

    // do stuff with struct
    printf("animal image url: %s\n", animal.image_url);
    printf("animal fact: %s\n", animal.fact);
    
    // free animal struct once used
    an_cleanup(&animal);

    // global cleanup
    an_cleanup(NULL);

    return 0;
}
```

If you want an asynchronous request, try this example:

```c
#include "animality.h"

// our request callback function!
void callback(const animal_t * animal) {
    printf("animal image url: %s\n", animal->image_url);
}

int main() {
    // create separate thread for requesting to the API
    const an_thread_t thr = an_get_async(AN_DOG, &callback);

    // this will run while the thread is still requesting to the API
    printf("Hello, World!\n");

    // wait for thread to terminate before we exit the main function
    an_thread_wait(thr);
    
    // global cleanup
    an_cleanup(NULL);
    
    return 0;
}
```

## [Rust]()
### Installation
```bash
$ echo :tada:
```

### Example
We use [`tokio`](https://tokio.rs) to help with the asynchronous runtime for Rust.

```rust
async fn main() -> Result<(), Box<dyn std::error::Error>> {
    let animality = Animality::new("API_KEY");
    let image = animality.fetch_random_image(String::from("capybara")).await?;
    let fact = animality.fetch_fact(String::from("capybara")).await?;

    println!("{}", image.link);
    println!("{}", fact.fact);

    Ok(());
}
```

This outputs the following text in the terminal:

```json
{
  "link": "https://api.animality.xyz/images/capybara/20.png",
  "fact": "Capybaras can make for good pets when kept in groups."
}
```
