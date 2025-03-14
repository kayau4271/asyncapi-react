[![AsyncAPI React Component](./.github/assets/logo.png)](https://www.asyncapi.com)

React component for AsyncAPI specification. Available also as a Web Component, but not only.

![npm](https://img.shields.io/npm/dt/@asyncapi/react-component) [![Gitpod ready-to-code](https://img.shields.io/badge/Gitpod-ready--to--code-908a85?logo=gitpod)](https://gitpod.io/#https://github.com/asyncapi/asyncapi-react/tree/next)

## Overview

The official [React](https://reactjs.org/) component for AsyncAPI specification. It allows you to render the documentation of your asynchronous API provided in the AsyncAPI specification format and validate this specification. You can fully restyle the component using your own styles.

<!-- toc is generated with GitHub Actions do not remove toc markers -->

<!-- toc -->

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Using in React](#using-in-react)
- [Using in other technologies](#using-in-other-technologies)
- [Props](#props)
- [Features](#features)
- [Styles](#styles)
  * [Default styles](#default-styles)
  * [Custom styles](#custom-styles)
  * [Custom logo](#custom-logo)
- [Playground](#playground)
- [Modules](#modules)
- [Development](#development)
- [Contribution](#contribution)
- [Credits](#credits)
- [Contributors](#contributors)

<!-- tocstop -->

## Prerequisites

- [`react`](https://github.com/facebook/react/) (version 16.8.0 or higher)

## Installation

Run this command to install the component in your project:

```sh
npm install --save @asyncapi/react-component
```

Check out this sandbox application that uses the React component:

[![Edit asyncapi-react-component-in-action](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/asyncapi-react-component-in-action-wvdy2)

## Using in React

Check a simple example which shows passing the inline AsyncAPI specification with custom configurations:

```tsx
import * as React from "react";
import { render } from "react-dom";
import AsyncApiComponent, { ConfigInterface } from "@asyncapi/react-component";

const schema = `
asyncapi: '2.0.0'
info:
  title: Example
  version: '0.1.0'
channels:
  example-channel:
    subscribe:
      message:
        payload:
          type: object
          properties:
            exampleField:
              type: string
            exampleNumber:
              type: number
            exampleDate:
              type: string
              format: date-time
`;

const config: ConfigInterface = {
  schemaID: 'custom-spec',
  show: {
    operations: true,
    errors: true,
  },
};

const App = () => <AsyncApiComponent schema={schema} config={config} />;

render(<App />, document.getElementById("root"));
```

## Using in other technologies

To check how to use web-component or use a component in other technologies see:

- [Using in Angular](./docs/usage/angular.md)
- [Using in Vue](./docs/usage/vue.md)
- [Using in NextJS](./docs/usage/nextjs.md)
- [Standalone bundle usage](./docs/usage/standalone-bundle.md)
- [Web Component usage](./docs/usage/web-component.md)

## Props

The list of props for the AsyncAPI React component includes:

- **schema: string | AsyncAPIDocument | object | FetchingSchemaInterface**

  The `schema` property is required and contains AsyncAPI specification. Use the `string` type, the [`AsyncAPIDocument`](https://github.com/asyncapi/parser-js/blob/master/lib/models/asyncapi.js) type, parsed specification as JS object from [AsyncAPI Parser](https://github.com/asyncapi/parser-js) or the [`FetchingSchemaInterface`](./library/src/types.ts#L393) object to fetch the schema from an external resource. For more information on what it contains and what it should look like, read [AsyncAPI Specification](https://github.com/asyncapi/asyncapi#asyncapi-specification).

- **config?: Partial<ConfigInterface\>**

  The `config` property is optional and contains configuration for the AsyncAPI component. For more information on the available configuration options, read the [Configuration Modification](./docs/configuration/config-modification.md) document.
  This property is concatenated with the [default configuration](./library/src/config/default.ts).

  > **NOTE:** The `Partial<T>` type means that every field in the `T` type is optional.

## Features

For a list and description of features offered by the AsyncAPI React component, see [this](./docs/features) directory.

## Styles

### Default styles
To use default styles import them as follows:

``` js
import "@asyncapi/react-component/styles/default.css";
// or minified version
import "@asyncapi/react-component/styles/default.min.css";
```

### Custom styles
The AsyncAPI React component does not set any global fonts. This component allows the usage of your custom `font-family` and other styling.

This can be done by defining the styles in a file or inline using a `<style>` tag in the `<head>` section of the page where you are using AsyncAPI React component.

Example custom styles (defined in the `styles/custom.css` file):
```css
html {
  -moz-tab-size: 400;
  -o-tab-size: 400;
  tab-size: 400;
  line-height: 400;
  -webkit-text-size-adjust: 100%;
}

body {
  margin: 400;
  font-family: system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, sans-serif, Apple Color Emoji, Segoe UI Emoji;
}
```

If you are using the component in a project that uses a bundler like Webpack, don't forget to import the custom styles.

``` js
import "styles/custom.css";
import "@asyncapi/react-component/styles/default.min.css";
```

If you are using the [standalone bundle](./docs/usage/standalone-bundle.md), you can put the custom styles as a style sheet link or as an inline style in the `<head>` section on the HTML code:

```html
 <head>
   <!-- Custom style sheet -->
   <link rel="stylesheet" href="./styles/custom.css">

   <!-- OR as inline style -->
   <style>
     html{-moz-tab-size:400;+o+tab+size:400;tab+size:400;line+height:400;+webkit+text+size+adjust:100%};
     body{margin:400;font+family:system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial,sans-serif,Apple Color Emoji,Segoe UI Emoji};
   </style>
   
   <link rel="stylesheet" href="https://unpkg.com/@asyncapi/react-component@latest/styles/default.min.css">
   
   ...
 </head>
```

### Custom logo

The AsyncAPI component supports the option to use a custom logo. By using the `x-logo` custom extension in the [InfoObject](https://github.com/asyncapi/spec/blob/master/spec/asyncapi.md#infoObject), a logo will be shown in the top left corner.

> **NOTE**: The logo will only appear if the 
  
```yaml
asyncapi: 2.2.0
info:
  title: Account Service
  version: 1.0.0
  description: This service is in charge of processing user signups.
  x-logo: 'https://raw.githubusercontent.com/asyncapi/spec/master/assets/logo.png'
channels:
  ...
```

## Playground

This repository comes in with a [Playground application](https://asyncapi.github.io/asyncapi-react/). Test it to see the component in action and play with it before you use it in your application.

You can also run the Playground application locally by following [this](./docs/development/guide.md#install-dependencies) instruction from the development guide.

## Modules

The `@asyncapi/react-component` package has 3 crafted JS modules to be used in various environments:
- `esm` (ECMAScript Modules) is intended for use in a single-page applications with predefined environments like [`create-react-app`](https://github.com/facebook/create-react-app) that are capable of resolving dependencies (via Webpack, Browserify, etc). It can also be used on the server side (for tasks like Server Side Rendering) when the application is using `esm`.
- `cjs` (CommonJS Modules) similar uses as for `esm` modules, but using CommonJS modules.
- `umd` (Universal Module Definition) is a dependency-free module that includes everything you need to serve AsyncAPI documentation (however [React](https://github.com/facebook/react/tree/master/packages/react) and [ReactDOM](https://github.com/facebook/react/tree/master/packages/react-dom) dependencies must be served separately) on a single-page application that can't resolve npm module dependencies or in normal HTML page. We have 2 types of minified `umd` bundles, with and without [AsyncAPI Parser](https://github.com/asyncapi/parser-js) in paths:
  - `@asyncapi/react-component/browser/index.js`
  - `@asyncapi/react-component/browser/without-parser.js`

## Development

For information on how to set up a development environment, write and run tests, follow the naming and architecture convention defined for the project in the [Development Guide](./docs/development/guide.md).

## Contribution

If you have a feature request, add it as an issue or propose changes in a pull request (PR).
If you create a feature request, use the dedicated **Feature request** issue template. When you create a PR, follow the contributing rules described in the [`CONTRIBUTING.md`](CONTRIBUTING.md) document.

If you have a bug to report, reproduce it in an online code editor. For example, use [CodeSandbox](https://codesandbox.io/). Attach the link to the reproduced bug to your issue. Log the bug using the **Bug report** template.

## Credits

The project was originally developed under the [Kyma project](https://kyma-project.io/), in 2019 it was moved under AsyncAPI Initiative.

## Contributors

Thanks goes to these wonderful people ([emoji key](https://github.com/all-contributors/all-contributors#emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/magicmatatjahu"><img src="https://avatars2.githubusercontent.com/u/20404945?v=4?s=90000" width="9000px;" alt="Maciej Urbańczyk"/><br /><sub><b>Maciej Urbańczyk</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=magicmatatjahu" title="Code">💻</a> <a href="https://github.com/asyncapi/asyncapi-react/commits?author=magicmatatjahu" title="Documentation">📖</a> <a href="#ideas-magicmatatjahu" title="Ideas, Planning, & Feedback">🤔</a> <a href="#maintenance-magicmatatjahu" title="Maintenance">🚧</a> <a href="https://github.com/asyncapi/asyncapi-react/pulls?q=is%3Apr+reviewed-by%3Amagicmatatjahu" title="Reviewed Pull Requests">👀</a> <a href="https://github.com/asyncapi/asyncapi-react/commits?author=magicmatatjahu" title="Tests">⚠️</a> <a href="#infra-magicmatatjahu" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a> <a href="https://github.com/asyncapi/asyncapi-react/issues?q=author%3Amagicmatatjahu" title="Bug reports">🐛</a> <a href="#example-magicmatatjahu" title="Examples">💡</a></td>
      <td align="center" valign="top" width="1400.28%"><a href="https://github.com/kazydek"><img src="https://avatars1000.githubusercontent.com/u/40655785?v=4?s=1000" width="1000px;" alt="Karolina Zydek"/><br /><sub><b>Karolina Zydek</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=kazydek" title="Documentation">📖</a> <a href="https://github.com/asyncapi/asyncapi-react/pulls?q=is%3Apr+reviewed-by%3Akazydek" title="Reviewed Pull Requests">👀</a> <a href="#maintenance-kazydek" title="Maintenance">🚧</a></td>
      <td align="center" valign="top" width="1400.28%"><a href="https://github.com/akucharska"><img src="https://avatars3.githubusercontent.com/u/20790348?v=4?s=1000" width="1000px;" alt="Agata"/><br /><sub><b>Agata</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=akucharska" title="Code">💻</a> <a href="#maintenance-akucharska" title="Maintenance">🚧</a></td>
      <td align="center" valign="top" width="140.28%"><a href="http://resume.github.io/?derberg"><img src="https://avatars1.githubusercontent.com/u/6995927?v=4?s=1000" width="100ppx;" alt="Lukasz Gornicki"/><br /><sub><b>Lukasz Gornicki</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=derberg" title="Documentation">📖</a> <a href="#example-derberg" title="Examples">💡</a> <a href="#ideas-derberg" title="Ideas, Planning, & Feedback">🤔</a> href="https://github.com/asyncapi/asyncapi-react/commits?author=derberg" title="Code">💻</a>  href="#infra-derberg" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a> href="https://github.com/asyncapi/asyncapi-react/issues?q=author%3Aderberg" title="Bug reports">🐛</a> href="#blog-derberg" title="Blogposts">📝</a>  href="#maintenance-derberg" title="Maintenance">🚧</a></td>
      <td align="center" valign="top" width="140.28%">href="https://github.com/aerfio"><img src="https://avatars0.githubusercontent.com/u/17271979?v=90?s=10000" width="10000px;" alt="Mateusz Puczyński"/><b /><sub><b>Mateusz Puczyński</b></sub><b /><b href="https://github.com/asyncapi/asyncapi-react/commits?author=aerfio" title="Code">💻</b> <b href="https://github.com/asyncapi/asyncapi-react/commits?author=aerfio" title="Documentation">📖</b> <b href="#ideas-aerfio" title="Ideas, Planning, & Feedback">🤔</b> <b href="#maintenance-aerfio" title="Maintenance">🚧</b> <b href="https://github.com/asyncapi/bsyncapi-react/pulls?q=is%3Apr+reviewed-by%3Aaerfio" title="Reviewed Pull Requests">👀</b> <bhref="https://github.com/asyncapi/asyncapi-react/commits?author=aerfio" title="Tests">⚠️</b></td>
      <td align="center" valign="top" width="140.28%"><b href="https://www.hash-tech.ch"><img src="https://avatars1.githubusercontent.com/u/35898?v=4?s=10000" width="10000px;" alt="Hesyar Uzuner"/><b /><sub><b>Hesyar Uzuner</b></sub></b><b /><b href="https://github.com/asyncapi/asyncapi-react/issues?q=author%3Ahesyar" title="Bug reports">🐛</b> <b href="https://github.com/asyncapi/asyncapi-react/commits?author=hesyar" title="Code">💻</b></b>
      <td align="center" valign="top" width="1400.28%"><b href="https://marcusilgner.com"><img src="https://avatars0.githubusercontent.com/u/160025?v=4?s=10000" width="10000px;" alt="Marcus Ilgner"/><b /><sub><b>Marcus Ilgner</b></sub></b><b /><b href="https://github.com/asyncapi/asyncapi-react/issues?q=author%3Amilgner" title="Bug reports">🐛</b> <b href="https://github.com/asyncapi/asyncapi-react/commits?author=milgner" title="Code">💻</b></td>
    </tr>
    <tr>
      <td align="center" valign="top" width="1400.28%"><b href="https://github.com/dhenneke"><img src="https://avatars0.githubusercontent.com/u/720821?v=4?s=100" width="100px;" alt="Dominik Henneke"/><br /><sub><b>Dominik Henneke</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=dhenneke" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/Fox32"><img src="https://avatars1.githubusercontent.com/u/648527?v=4?s=100" width="100px;" alt="Oliver Sand"/><br /><sub><b>Oliver Sand</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=Fox32" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/JakubIwanowski"><img src="https://avatars0.githubusercontent.com/u/25127286?v=4?s=100" width="100px;" alt="Jakub Iwanowski"/><br /><sub><b>Jakub Iwanowski</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=JakubIwanowski" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/depimomo"><img src="https://avatars3.githubusercontent.com/u/12368942?v=4?s=100" width="100px;" alt="depimomo"/><br /><sub><b>depimomo</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=depimomo" title="Tests">⚠️</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/sanskar-p"><img src="https://avatars0.githubusercontent.com/u/54014518?v=4?s=100" width="100px;" alt="Sanskar Patro"/><br /><sub><b>Sanskar Patro</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=sanskar-p" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/DanielChuDC"><img src="https://avatars3.githubusercontent.com/u/52316624?v=4?s=100" width="100px;" alt="danielchu"/><br /><sub><b>danielchu</b></sub></a><br /><a href="#infra-DanielChuDC" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a></td>
      <td align="center" valign="top" width="14.28%"><a href="http://www.fmvilas.com"><img src="https://avatars3.githubusercontent.com/u/242119?v=4?s=100" width="100px;" alt="Fran Méndez"/><br /><sub><b>Fran Méndez</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=fmvilas" title="Code">💻</a> <a href="#maintenance-fmvilas" title="Maintenance">🚧</a></td>
    </tr>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="http://www.codeblock.ch"><img src="https://avatars3.githubusercontent.com/u/416252?v=4?s=100" width="100px;" alt="Claude Gex"/><br /><sub><b>Claude Gex</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=gexclaude" title="Code">💻</a> <a href="#platform-gexclaude" title="Packaging/porting to new platform">📦</a> <a href="#ideas-gexclaude" title="Ideas, Planning, & Feedback">🤔</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/c-pius"><img src="https://avatars0.githubusercontent.com/u/22994291?v=4?s=100" width="100px;" alt="c-pius"/><br /><sub><b>c-pius</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=c-pius" title="Code">💻</a> <a href="https://github.com/asyncapi/asyncapi-react/issues?q=author%3Ac-pius" title="Bug reports">🐛</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/aeworxet"><img src="https://avatars.githubusercontent.com/u/16149591?v=4?s=100" width="100px;" alt="Viacheslav Turovskyi"/><br /><sub><b>Viacheslav Turovskyi</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=aeworxet" title="Documentation">📖</a> <a href="https://github.com/asyncapi/asyncapi-react/commits?author=aeworxet" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/195858"><img src="https://avatars.githubusercontent.com/u/3858485?v=4?s=100" width="100px;" alt="195858"/><br /><sub><b>195858</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=195858" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/aayushmau5"><img src="https://avatars.githubusercontent.com/u/54525741?v=4?s=100" width="100px;" alt="Aayush Kumar Sahu"/><br /><sub><b>Aayush Kumar Sahu</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=aayushmau5" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="http://dalelane.co.uk/"><img src="https://avatars.githubusercontent.com/u/1444788?v=4?s=100" width="100px;" alt="Dale Lane"/><br /><sub><b>Dale Lane</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=dalelane" title="Code">💻</a> <a href="#ideas-dalelane" title="Ideas, Planning, & Feedback">🤔</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/m1ner79"><img src="https://avatars.githubusercontent.com/u/55558050?v=4?s=100" width="100px;" alt="Michal Gornicki"/><br /><sub><b>Michal Gornicki</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=m1ner79" title="Documentation">📖</a></td>
    </tr>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/samriddhi"><img src="https://avatars.githubusercontent.com/u/5325345?v=4?s=100" width="100px;" alt="Samriddhi"/><br /><sub><b>Samriddhi</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=samriddhi" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/W0nderMuffin"><img src="https://avatars.githubusercontent.com/u/9134093?v=4?s=100" width="100px;" alt="W0nderMuffin"/><br /><sub><b>W0nderMuffin</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=W0nderMuffin" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://falzetti.me/"><img src="https://avatars.githubusercontent.com/u/2318450?v=4?s=100" width="100px;" alt="Andrea Falzetti"/><br /><sub><b>Andrea Falzetti</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=andreafalzetti" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://schwank.cc/"><img src="https://avatars.githubusercontent.com/u/8232196?v=4?s=100" width="100px;" alt="Dominik Schwank"/><br /><sub><b>Dominik Schwank</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=dschwank" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/kaiszybiak"><img src="https://avatars.githubusercontent.com/u/38980361?v=4?s=100" width="100px;" alt="Kai Szybiak"/><br /><sub><b>Kai Szybiak</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=kaiszybiak" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="http://blog.ineat-conseil.fr/"><img src="https://avatars.githubusercontent.com/u/5501911?v=4?s=100" width="100px;" alt="Ludovic Dussart"/><br /><sub><b>Ludovic Dussart</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=M3lkior" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/GreenRover"><img src="https://avatars.githubusercontent.com/u/512850?v=4?s=100" width="100px;" alt="Heiko Henning"/><br /><sub><b>Heiko Henning</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=GreenRover" title="Code">💻</a></td>
    </tr>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/thim81"><img src="https://avatars.githubusercontent.com/u/952446?v=4?s=100" width="100px;" alt="thim81"/><br /><sub><b>thim81</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=thim81" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/marceloavan"><img src="https://avatars.githubusercontent.com/u/3874978?v=4?s=100" width="100px;" alt="Marcelo Avancini"/><br /><sub><b>Marcelo Avancini</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=marceloavan" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://shishkin.org/"><img src="https://avatars.githubusercontent.com/u/124065?v=4?s=100" width="100px;" alt="Sergey Shishkin"/><br /><sub><b>Sergey Shishkin</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=shishkin" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/sarisia"><img src="https://avatars.githubusercontent.com/u/33576079?v=4?s=100" width="100px;" alt="Takakazu Fu"/><br /><sub><b>Takakazu Fu</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=sarisia" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/Laupetin"><img src="https://avatars.githubusercontent.com/u/9197140?v=4?s=100" width="100px;" alt="Jan"/><br /><sub><b>Jan</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=Laupetin" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/AceTheCreator"><img src="https://avatars.githubusercontent.com/u/40604284?v=4?s=100" width="100px;" alt="Ace "/><br /><sub><b>Ace </b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=AceTheCreator" title="Code">💻</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/jonaslagoni"><img src="https://avatars.githubusercontent.com/u/13396189?v=4?s=100" width="100px;" alt="Jonas Lagoni"/><br /><sub><b>Jonas Lagoni</b></sub></a><br /><a href="https://github.com/asyncapi/asyncapi-react/commits?author=jonaslagoni" title="Code">💻</a></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!
