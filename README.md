# Hollywood Code Editor
The **Hollywood Code Editor** is a lightweight extensible code editor targeting the Lua programming language. Built around [`monaco-editor-core`](https://www.npmjs.com/package/monaco-editor-core) and sumneko's [`lua-language-server`](https://github.com/sumneko/lua-language-server), its modular design allows anybody to integrate the Hollywood Code Editor into their development toolchain with the features that are relevant to them. It is also customizable in pretty much every foreseeable way, offering a beautiful design language modeled after [Fluent UI](https://developer.microsoft.com/en-us/fluentui#/).

The Hollywood Code Editor does not directly include any facilities that permits the execution of Lua code, as to let users implement their own interfaces to the Lua distribution of their choice. This can be done by writing a plugin module that can then be consumed by the interface to implement execution behavior, which requires minimal effort. 

**Note:** This is a partial release meant to distribute auxiliary files related to Hollywood, such as stylesheets, for preparatory and demonstration purposes. The full release of the interface will proceed upon its commerical distribution becoming publicly availabie.

# Feature Overview
- **Full editor stack** featuring support for the [Language Server Protocol](https://microsoft.github.io/language-server-protocol/overviews/lsp/overview/) using [JSON-RPC](https://www.jsonrpc.org/specification) over sockets. Our interface includes [`monaco-editor-core`](https://www.npmjs.com/package/monaco-editor-core), the core and central component of Visual Studio Code's powerful text editor that we wired to [`monaco-languageclient`](https://github.com/TypeFox/monaco-languageclient), a complete and easy-to-use LSP client, alongside our own extensions to either package. Included with Hollywood is a distribution of [lsp-ws-proxy](https://github.com/qualified/lsp-ws-proxy) that allows you to proxify stdio-oriented language servers to websockets, guaranteeing our stack's full support for most language servers.
- **A flexible and modular codebase** that offers a straightforward plugin-loading mechanism system allowing developers to quickly and easily extend the functionality of the code editor. You can look at `src/modules_renderer/template.ts` for more information.
- **A relatively simple package and repository** system that allows developers to include third-party Lua code into their projects without having to use specialized Lua runtimes or library extensions. The packaging, depackaging and sewing-up of files is done entirely by Hollywood.
- **Versatile theming**. The design of practically every element is defined by the `hollywood-*` collection of stylesheets, and interface settings allows users to easily load in custom CSS deployed to `/themes`. There is no official support for loading in user-provided HTML files due to security concerns, but they are able to manually replace assets in the application's installation directory if desired.

# Notes
- The Hollywood Code Editor is for **standalone desktop distribution only** and is unlikely to work in a browser environment. Considering the weight of the editor, we wouldn't recommend trying to adapt it (or any of its components) for a browser environment anyway. If you want to include the base editor used by Hollywood, we suggest you take a look at [monaco-editor](https://github.com/microsoft/monaco-editor), which supports far more languages than Hollywood's distribution that only supports Lua.
- Hollywood automatically applies a number of rudimentary patches to JavaScript's module import system that may break the code editor if the project is bundled with [Webpack](https://github.com/webpack/webpack) or other similar solutions. Theses patches are to resolve incompatibilities between packages used by the Hollywood code editor.
# Installation
Development and installation requires `nodejs` v14 and above alongside Build Tools for Visual Studio (2019 and above). There is no need to install Visual Studio in its entirety - only the commandline build tools offered on that page. 
- You can download `nodejs` v14 and above [here](https://nodejs.org/en/). Newer is better unless indicated otherwise on this readme, or enforced programmatically in `package.json`. Either way, you will get a nice error if there is cause.
- You can download `Build Tools for Visual Studio` (2019 and above) [here](https://visualstudio.microsoft.com/downloads/?q=build+tools). As mentioned above, you do not have to install Visual Studio itself, only the build tools found at the bottom of the page.

Before building the Hollywood code editor, you must install all dependencies using `npm i` in a terminal pointing to the root directory. You can then build and run the application using `npm run start` (this  will always perform a build - if you're looking to run any code already compiled, you can use `start-prebuilt` instead). The output directory is `/build`.

# Packaging
To package the Hollywood code editor for distribution, you can use the command `npm run package`. This will output 32-bit Windows binaries in `/out/synapsex-win32-ia32/` using [`electron-forge`](https://github.com/electron-userland/electron-forge) that can be archived and sent to people. You can configure packaging options in `package.json`.
# Licensing
The Hollywood Code Editor is licensed under the [GNU Affero General Public License Version 3](https://www.gnu.org/licenses/agpl-3.0.txt). The Hollywood Code Editor is free software: you can redistribute it and/or modify it under the terms of the GNU Affero General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version. The Hollywood Code Editor is distributed in the hope that it will be useful, but without any warranty; without even the implied warranty of merchantability or fitness for a particular purpose. See the [GNU Affero General Public License Version 3](https://www.gnu.org/licenses/agpl-3.0.txt) for more details.
