# 🗜️⚡ wasm-flate  [![Tweet](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/intent/tweet?text=The%20fastest%20compression%20library%20in%20your%20browser.&url=https://github.com/drbh/wasm-flate&hashtags=wasm,js,webdev,rust,compression)

<img src="https://raw.githubusercontent.com/drbh/wasm-flate/master/images/wasm-flate.png" width="320" />

[![npm version](https://badge.fury.io/js/wasm-flate.svg)](https://badge.fury.io/js/wasm-flate)
[![dependencies Status](https://david-dm.org/dwyl/esta/status.svg)](https://david-dm.org/dwyl/esta)

The fastest compression and decompression in the browser.

## Installation

Load it into node
```
npm i wasm-flate
```

Or use it in you HTML page with the precompiled CDN version
```html
<script src="https://unpkg.com/wasm-flate@0.1.11-alpha/dist/bootstrap.js"></script>
```

### For server side code 
check out the examples for code to decompress data in Python, Node and Go on the server side

## Resources
[Docs](https://github.com/drbh/wasm-flate/blob/master/DOCS.md) - get API reference and flate functions.  

[Examples](https://github.com/drbh/wasm-flate-examples) - Examples compressing in browser, sending to node server and decompressing... really fast!  

## Example Screenshot

![File Upload and Compress UI](https://raw.githubusercontent.com/drbh/wasm-flate-examples/master/images/fileinput.png)


### Compared to JS implementation (pako)

Test `pako` vs `wasm-flate` in your browsers [here](http://wasm-flate.s3-website-us-east-1.amazonaws.com/)

![image](https://raw.githubusercontent.com/drbh/wasm-flate/master/images/compare.png)

In Chrome on my MacBook Pro, we see that pako takes about 143 ms where `wasm-flate` only takes about 21 ms. This is 6.8x faster.  

# Why use `wasm-flate`

## WASM npm library for fast (de)compression

- Uses WASM  
- As fast as C or Rust implementation  
- Works in all browsers  
- GZIP supported  
- ZLIB supported  
- DELFATE supported  

### Uses
- Shipping compressed data from server and decompress in browser
- Shipping compressed data to server by compressing in browser
- Better UX for mobile (fast decompress - slow data fetch)
- Better UX for people with sparse networks   
- Less resource use on server side  
- Decreased storage need  
- Leveraging growing WASM ecosystem  

This package allows you to quickly compress and decompress data in the browser. The process is simple and optmized to execute as fast as your browser can run.

#### Compress
Pass a string or Uint8Array to the compression function you choose. The contents will be compressed and encoded to base64. The returned value will be a base64 encoded string.

#### Decompress
Pass a base64 string of the compressed data and it will return a base64 decompressed value.  


# Example Node use

```javascript
var flate = require('wasm-flate');

var data = "THIS IS EXAMPLE DATA TO COMPRESS"
var compressed_data = flate.zlib_encode(data)
var original_data = flate.zlib_decode(compressed_data)
```

### Full Use Example

This will read in the string as a u8array, compress, decompress and compare the output with the original value. This show cases all the main uses of `wasm-flate`  

```javascript
var flate = require('wasm-flate');
var data = new Uint8Array( Buffer.from('wasm-flate is awesome!') );
var comp = flate.deflate_encode_raw(data)
var decomp = flate.deflate_decode_raw(comp)
JSON.stringify(data) === JSON.stringify(decomp) 
```

### Compressing Data

Here we can see how to compress data as a string, and it will return a base64 encoded compressed value.  

```javascript
var data = "THIS IS EXAMPLE DATA TO COMPRESS"
var compressed_data = flate.zlib_encode(data)
// this data is zlib compressed and base64 encoded
```

```javascript
var data = "THIS IS EXAMPLE DATA TO COMPRESS"
var compressed_data = flate.gzip_encode(data)
// this data is gzip compressed and base64 encoded
```

```javascript
var data = "THIS IS EXAMPLE DATA TO COMPRESS"
var compressed_data = flate.deflate_encode(data)
// this data is deflate compressed and base64 encoded
```

### Decompressing Data

```javascript
var original_data = flate.zlib_decode("eNrtlEtOAzEMhvc9RTXrLpw4jmMu0EMgFk7GQQjRSjCgSlXvThgG1KpqeUgskOpN/Ppt61tkO5vPu14H7a7m2+a3aHjU3p5afD3G8yk/1vRh/bwalja0cuco+kARE/lucdRz92JjEzgiiZEAE0y23337Pgs2xbhCzOo5o5GnUvpamrSYSotbrooztQPxtAQ2Kk6sFvbcjvK+AHt1JMFqnzU5TqoYoU/76mF9b6vlx36DzOK5BK0eOVLJ5NAFBQPyTiUGqmBejyd8HgHftG6asFt8QVgkCgglCKcBMzI7hCRB4t/xdQYphkwxclOElBO7LD2IQ8SqVjBgqLH+N77nuPoLzx/zxOTPMqWAGC5cf/sP4Gm2Cbj9ANzYBrzwPeQ7vjezN2/3Cpfxnx4=")
```

The folowing output is some compressed JSON of ECR20 tokens traded on a DEX (the data used is arbitrary!)  
```json
{
  "data": {
    "trades": [
      {
        "amountGet": "15624563852",
        "amountGive": "10155966503800000000",
        "get": "0xce7f06ba27b3e525ccdfc559cea9e523e5f91eae",
        "give": "0xa919efc72756222c072a1594efdba8178aa360d8",
        "tokenGet": "0xe0b7927c4af23765cb51314a0e0521a9645f0e2a",
        "tokenGive": "0x0000000000000000000000000000000000000000"
      }
  ], "..."
}
```

# Contributing

## Rough Roadmap

- [X] Compile compression to WASM  
- [X] Build useful functions for compression  
- [X] Compile useful functions to WASM  
- [X] Publish NPM package of WASM files and JS shim  
- [X] Add new functions for u8Array support  
- [X] Add basic API docs  
- [X] Write short medium article  
- [X] Compare with Native JS example  
- [X] Add node server side example  
- [X] Add Python server side example  
- [X] Make logo for lib based on WASM colorway  
- [ ] Deploy to WAPM  
- [ ] Add Golang example  
- [ ] Add benchmarking suite   
- [ ] Deploy multi file example  
- [ ] Release solid roadmap  
- [ ] Releae update schedule  
- [ ] Find partner for case study  



## Building with Rust 🦀🕸️ 

In order to build the wasm files with Rust, you'll need to clone the repo and run `wasm-pack` with `nodejs` as the target. This will create a set of files in `pkg` that can be used as a node module. 

```
git clone https://github.com/drbh/wasm-flate.git
cd wasm-flate
wasm-pack build --target nodejs
```

You should have the following new files  
```
pkg/
├── LICENSE-APACHE
├── LICENSE-MIT
├── README.md
├── wasm-flate.d.ts
├── wasm-flate.js
├── wasm-flate_bg.d.ts
├── wasm-flate_bg.js
├── wasm-flate_bg.wasm
└── package.json
```


## Donate Here
If you found `wasm-flate` useful feel free to buy me a beer 🍺 or two 😀  
`BTC - 3QVK6D5QCZDSyLzFL3ZbELokyuSprRQQZF`
