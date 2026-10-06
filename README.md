# NopeCHA Node.js Library

![NPM Version](https://img.shields.io/npm/v/nopecha?label=NPM&link=https%3A%2F%2Fnopecha.com&link=https%3A%2F%2Fnopecha.com%2Fnpm)
![PyPI - Version](https://img.shields.io/pypi/v/nopecha?label=PyPI&link=https%3A%2F%2Fnopecha.com&link=https%3A%2F%2Fnopecha.com%2Fpypi)
![GitHub Release](https://img.shields.io/github/v/release/NopeCHALLC/nopecha-extension?label=Extension%20Release&color=4a4&link=https%3A%2F%2Fnopecha.com&link=https%3A%2F%2Fnopecha.com%2Fgithub)
![Chrome Web Store Version](https://img.shields.io/chrome-web-store/v/dknlfmjaanfblgfdfebhijalfmhmjjjo?label=Chrome%20Web%20Store&color=4a4&link=https%3A%2F%2Fnopecha.com&link=https%3A%2F%2Fnopecha.com%2Fchrome)
![Mozilla Add-on Version](https://img.shields.io/amo/v/noptcha?label=Mozilla%20Add-on&color=4a4&link=https%3A%2F%2Fnopecha.com&link=https%3A%2F%2Fnopecha.com%2Ffirefox)

The NopeCHA Node.js library provides convenient access to the NopeCHA API
from applications written in the Node.js language. It includes a
pre-defined set of classes for API resources that initialize
themselves dynamically from API responses.

**Important note: this library is meant for server-side usage only, as using it in client-side browser code will expose your secret API key. [See here](https://developers.nopecha.com) for more details.**

## Supported CAPTCHA types:

- reCAPTCHA v2
- reCAPTCHA v3
- reCAPTCHA Enterprise
- FunCAPTCHA
- AWS WAF CAPTCHA
- Text-based CAPTCHA

## Documentation

See the [NopeCHA API docs](https://developers.nopecha.com).

## Installation

```bash
$ npm install nopecha
```

## Usage

The library needs to be configured with your account's secret key which is available on the [website](https://nopecha.com/manage). Either set it as the `NOPECHA_API_KEY` environment variable before using the library:

```bash
export NOPECHA_API_KEY='...'
```

Or set `nopecha.api_key` to its value:

```javascript
const { Configuration, NopeCHAApi } = require("nopecha");

const configuration = new Configuration({
  apiKey: process.env.NOPECHA_API_KEY,
});
const nopecha = new NopeCHAApi(configuration);

// solve a recognition challenge
const clicks = await nopecha.solveRecognition({
  type: "recaptcha",
  task: "Select all squares with vehicles.",
  image_urls: ["https://nopecha.com/image/demo/recaptcha/4x4.png"],
});

// print the grids to click
console.log(clicks);

// solve a token
const token = await nopecha.solveToken({
  type: "recaptcha",
  sitekey: "6Ld8NA8jAAAAAPJ_ahIPVIMc0C4q58rntFkopFiA",
  url: "https://nopecha.com/demo/recaptcha#easy",
});

// print the token
console.log(token);

// get the current balance
const balance = await nopecha.getBalance();

// print the current balance
console.log(balance);
```
