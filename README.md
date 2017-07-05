# tiny-cookie

[![Build Status](https://travis-ci.org/Alex1990/tiny-cookie.svg?branch=master)](https://travis-ci.org/Alex1990/tiny-cookie)

A tiny cookie manipulation plugin for browser.

## Packages

**NPM:**

```bash
npm install tiny-cookie
```

**Bower:**

```bash
bower install tiny-cookie
```

## Usage

**ES2015 (recommended)**

```js
// You can import all methods.
import * as Cookies from 'tiny-cookie'

// Or, you can import the methods as needed.
import { isEnabled, get, set, remove } from 'tiny-cookie'

// No alias required, just imports.
import { isCookieEnabled, getCookie, setCookie, removeCookie } from 'tiny-cookie'
```

The tiny-cookie will expose a method `Cookie` on the global scope. Also, it can be as a CommonJS/AMD module (**recommended**).

## APIs

### isEnabled()

**Alias: isCookieEnabled**

Check if the cookie is enabled.

### get(key)

**Alias: getCookie**

Get the cookie value with decoding, using `decodeURIComponent`.

### getRaw(key)

**Alias: getRawCookie**

Get the cookie value without decoding.

### getAll()

**Alias: getAllCookies**

Get all cookies with decoding, using `decodeURIComponent`.

### set(key, value, options)

**Alias: setCookie**

Set a cookie with encoding the value, using `encodeURIComponent`. The `options` parameter is an object. And its property can be a valid cookie option, such as `path`(default: root path `/`), `domain`, `expires`/`max-age` or `secure` (Note: the `secure` flag will be set if it is an truthy value, such as `true`, or it will be not set). For example, you can set the expiration:

```js
import { setCookie } from 'tiny-cookie';

const now = new Date;
now.setMonth(now.getMonth() + 1);

setCookie('foo', 'Foo', { expires: now.toGMTString() });
```

The `expires` property value can accept a `Date` object, a parsable date string (parsed by `Date.parse()`), an integer (unit: day) or a numeric string with a suffix character which specifies the time unit.

| Unit suffix | Representation |
| ----------- | -------------- |
| Y           | One year       |
| M           | One month      |
| D           | One day        |
| h           | One hour       |
| m           | One minute     |
| s           | One second     |

**Examples:**

```js
const { setCookie } from 'tiny-cookie';
const date = new Date;

date.setDate(date.getDate() + 21);

setCookie('dateObject', 'A date object', { expires: date });
setCookie('dateString', 'A parsable date string', { expires: date.toGMTString() });
setCookie('integer', 'Seven days later', { expires: 7 });
setCookie('stringSuffixY', 'One year later', { expires: '1Y' });
setCookie('stringSuffixM', 'One month later', { expires: '1M' });
setCookie('stringSuffixD', 'One day later', { expires: '1D' });
setCookie('stringSuffixh', 'One hour later', { expires: '1h' });
setCookie('stringSuffixm', 'Ten minutes later', { expires: '10m' });
setCookie('stringSuffixs', 'Thirty seconds later', { expires: '30s' });
```

### setRaw(key, value, options)

**Alias: setRawCookie**

Set a cookie without encoding.

### remove(key)

**Alias: removeCookie**

Remove a cookie.

## FAQ

1. How to use JSON as the encoder/decoder?

You can write your cookie get and set methods with JSON support easily:

```js
import { getCookie, setCookie } from 'tiny-cookie';

export const getJSON = (key) => getCookie(key, JSON.parse);
export const setJSON = (key, value, options) => setCookie(key, value, JSON.stringify, options);
```

## License

MIT.
