# svelte-nodegui-wasm-starter

**Clone and run for a quick way to see Svelte NodeGui + Wasm in action.**

This is a fork of the [svelte-nodegui-starter](https://github.com/nodegui/svelte-nodegui-starter) repo with the addition of using WASM with Rust.  Note, this currently breaks hot reloading.

<img alt="logo" src="https://raw.githubusercontent.com/bradyjoslin/svelte-nodegui-wasm-starter/main/assets/demo.png" height="500" />

## To Use

To clone and run this repository you'll need [Git](https://git-scm.com) and [Node.js](https://nodejs.org/en/download/) (which comes with [npm](http://npmjs.com)) installed on your computer.

Make sure you have met the requirements listed here: https://docs.nodegui.org/#/tutorial/development-environment

Additionally, you'll need to have [Rust](https://www.rust-lang.org/) and [wasm-pack](https://rustwasm.github.io/wasm-pack/installer/) installed.

From your command line:

```bash
# Create a copy of this repository (or just clone)
npx degit bradyjoslin/svelte-nodegui-wasm-starter my-app
# Go into the project's crate directory
cd my-app/crate
wasm-pack build
# Go into the project root directory
cd ../
# Install dependencies
npm install
# Build the app in development mode (unminified; watch mode on)
npm run dev
# (From another terminal) Run the built app
npm run start
```

## Wasm Interaction

A greet function is exposed in `crate/src/lib.rs`, which takes a string as an argument:

```rust
#[wasm_bindgen]
pub fn greet(name: &str) -> String {
    format!("Welcome to {} 🐕", name)
}
```

The Wasm package is imported, the greet function is called, and the result is rendered to the screen in `src/App.svelte`

```js
// ...

import * as wasm from '../crate/pkg'

let hi = wasm.greet("Svelte NodeGUI + WASM");

// ...

    <view style="flex: 1;">
        <text id="welcome-text">{hi}</text>
        <text id="step-1">1. Play around</text>
        <StepOne />
        <text id="step-2">2. Debug</text>
        <StepTwo />
    </view>

// ...
```

## Resources for Learning NodeGui

- [svelte.nodegui.org](https://svelte.nodegui.org) - all of Svelte NodeGui's documentation

## Resources for Learning wasm-pack

- [wasm-pack docs](https://rustwasm.github.io/docs/wasm-pack/introduction.html)

## Packaging app as a distributable

In order to distribute your finished app, you can use [@nodegui/packer](https://github.com/nodegui/packer)

### Step 1: (_**Run this command only once**_)

```sh
npx nodegui-packer --init MyAppName
```

This will produce the deploy directory containing the template. You can modify this to suite your needs. Like add icons, change the name, description and add other native features or dependencies. Make sure you commit this directory.

### Step 2: (_**Run this command every time you want to build a new distributable**_)

Next you can run the pack command:

```sh
npm run build
```

This will produce the js bundle along with assets inside the `./dist` directory

```sh
npx nodegui-packer --pack ./dist
```

This will build the distributable using `@nodegui/packer` based on your template. The output of the command is found under the build directory. You should gitignore the build directory.

More details about `@nodegui/packer` can be found here: https://github.com/nodegui/packer

## License

MIT
