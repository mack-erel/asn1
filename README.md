# `@yrneh_jang/asn1`

[![npm](https://img.shields.io/npm/v/@yrneh_jang/asn1)](https://www.npmjs.com/package/@yrneh_jang/asn1)

Fork of [`@ldapjs/asn1`](https://github.com/ldapjs/asn1) with **Cloudflare Workers support**.

## Changes from upstream

- `fs` module is lazy-loaded inside the function body instead of at module load time, so the package works in Cloudflare Workers where `fs` is not available.

## Installation

```sh
npm install @yrneh_jang/asn1
```

## Usage

### Decoding

```js
const { BerReader, BerTypes } = require('@yrneh_jang/asn1')
const reader = new BerReader(Buffer.from([0x30, 0x03, 0x01, 0x01, 0xff]))

reader.readSequence()
console.log('Sequence len: ' + reader.length)
if (reader.peek() === BerTypes.Boolean)
  console.log(reader.readBoolean())
```

### Encoding

```js
const { BerWriter } = require('@yrneh_jang/asn1')
const writer = new BerWriter()

writer.startSequence()
writer.writeBoolean(true)
writer.endSequence()

console.log(writer.buffer)
```

## Cloudflare Workers

No additional configuration needed. Works out of the box with `nodejs_compat` compatibility flag.

```toml
# wrangler.toml
compatibility_flags = ["nodejs_compat"]
```

## License

MIT
