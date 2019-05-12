---
title: "Typescript without Typscript"
date: "2019-05-11"
description: "ways you can use typescript without fully committing"
---

Typescript is fantastic. It will never be as sound as something like elm or haskell, but it is what it is, and you should probably use it.
The benifits of typescript itself can be read across the internet.
This post isn't the first or last to talk about typescript. What this post aims to achive is showing how you can _use typescript_ without having to fully
commit to writing typescript yourself.

Althought there are great projects like [parcel](https://parceljs.org/) and [tsdx](https://github.com/palmerhq/tsdx), setting up new (or even worse) or already-in-production apps to use typescript is not exactly easy. It takes time. Lots of confusing time.

### Setup

```shell
cd your-project #(or make new project)
npm init
npm install typescript --save-dev
npx tsc --init
```

Check out the options in the `tsconfig.json` file to get an understanding of the options.

After looking over `tsconfig.json`, make it look like this

```json
{
  "compilerOptions": {
    "target": "ESNEXT",
    "module": "es2015",
    "allowJs": true,
    "checkJs": true,
    "strict": true,
    "esModuleInterop": true
  }
}
```

Create `index.js`

```shell
touch index.js
```

Add some code to `index.js`

```javascript
function sumTwo(a, b) {
  return a + b
}
```

Now, if you're already using [vscode](https://code.visualstudio.com/), you will see where this is headed.

Run

```shell
npx tsc --noEmit
```

and you should see something like

```shell
λ npx tsc --noEmit
src/index.js:1:17 - error TS7006: Parameter 'a' implicitly has an 'any' type.

1 function sumTwo(a, b) {
                  ~

src/index.js:1:20 - error TS7006: Parameter 'b' implicitly has an 'any' type.

1 function sumTwo(a, b) {
```

## Closing

As you can see, without even having to fully invest in Typescript, you can still use it's compiler to help typecheck your code.

In future posts I want to also show:

- How you can interop with libraries
- How you can add types to your javascript files
- Why you might not need babel anymore
- Awesome integration with vscode
