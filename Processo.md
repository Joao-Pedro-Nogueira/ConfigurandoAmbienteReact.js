Passo a passo de todo o processo de configuração do ambiente.
Terminal: git bash

# Criando a estrutura do projeto

Comando no terminal:

```bash
npm init -y
```

Verificação:
arquivo 'package.json' criado na raiz.

Comando no terminal

```bash
npm add react react-dom
```

Verificação:
arquivo 'package-lock.json' e diretório 'node_modules' criados na raiz.

Criar: '.gitignore' na raiz.

```
node_modules
**/node_modules
```

Criar: diretórios 'src' e 'public' na raiz.

Criar: arquivo 'index.html' no 'public'

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Título</title>
  </head>
  <body></body>
</html>
```

# Configurando Babel

Comando no terminal:

```bash
npm add @babel/core @babel/cli @babel/preset-env -D
```

Verificação: verificar se as bibliotecas foram adicionadas no 'package.json'

Criar: arquivo 'babel.config.js' na raiz

```js
module.exports = {
  presets: ['@babel/preset-env']
}
```

Criar: arquivo 'index.jsx' na pasta 'src'

```js
const user = {
  name: 'Pedro'
}

console.log(user.address?.street)
```

Verificar se está tudo certo até agora:
Comando no terminal:

```bash
npx babel src/index.jsx -o dist/bundle.js
```

ou

```bash
npx babel src/index.jsx --out-file dist/bundle.js
```

Se a pasta 'dist' foi criada com o arquivo 'bundle.js' contendo:

```js
'use strict'

var _user$address

var user = {
  name: 'Pedro'
}
console.log(
  (_user$address = user.address) === null || _user$address === void 0
    ? void 0
    : _user$address.street
)
```

Então, está tudo certo até agora!

Alterar: arquivo .gitignore:

```
node_modules
**/node_modules
dist
```

## Instalando babel/preset-react

Comando no terminal:

```bash
npm add @babel/preset-react -D
```

Verificação: verificar se a biblioteca foi adicionada no 'package.json'

Alterar: arquivo 'babel.config.js'

```js
// babel.config.js
module.exports = {
  presets: ['@babel/preset-env', '@babel/preset-react']
}
```

Verificação:

```js
// src/index.js
import React from 'react'

function App() {
  return <h1>Hello World</h1>
}
```

Comando no terminal:

```bash
npx babel src/index.jsx -o dist/bundle.js
```

Se o comando alterar o arquivo 'dist/bundle.js' para:

```js
'use strict'

var _react = _interopRequireDefault(require('react'))

function _interopRequireDefault(obj) {
  return obj && obj.__esModule ? obj : { default: obj }
}

// src/index.js
function App() {
  return /*#__PURE__*/ _react['default'].createElement(
    'h1',
    null,
    'Hello World'
  )
}
```

Então está tudo certo!

# Configurando webpack

Comando no terminal:

```bash
npm add webpack webpack-cli webpack-dev-server -D
```

Verificação: verificar se foram adicionadas no 'package.json'

Criar: arquivo 'webpack.config.js' na raiz

```js
// webpack.config.js
const path = require('path')

module.exports = {
  entry: path.resolve(__dirname, 'src', 'index.jsx'),
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  resolve: {
    extensions: ['.js', '.jsx']
  },
  module: {
    rules: [
      {
        test: /\.jsx$/,
        exclude: /node_modules/,
        use: 'babel-loader'
      }
    ]
  }
}
```

### Adicionando babel-loader

Comando no terminal:

```bash
npm add babel-loader -D
```

Verificação: verificar se foram adicionadas no 'package.json'

## Teste de funcionamento

Criar: Arquivo 'App.jsx' na pasta 'src'

```js
// App.jsx
export function App() {
  return <h1>Hello World</h1>
}
```

Alterar: arquivo 'src/index.jsx'

```js
// src/index.js
import React from 'react'
import { App } from './App'
```

Comando no terminal:

```bash
npx webpack
```

Não tem problema ocorrer um WARNING.

Se o 'dist/bundle.js' foi alterado para:

```js
// dist/bundle.js
/*! For license information please see bundle.js.LICENSE.txt */
;(() => {
  'use strict'
  var t = {
      408: (t, e) => {
        Symbol.for('react.element'),
          Symbol.for('react.portal'),
          Symbol.for('react.fragment'),
          Symbol.for('react.strict_mode'),
          Symbol.for('react.profiler'),
          Symbol.for('react.provider'),
          Symbol.for('react.context'),
          Symbol.for('react.forward_ref'),
          Symbol.for('react.suspense'),
          Symbol.for('react.memo'),
          Symbol.for('react.lazy'),
          Symbol.iterator
        var o = {
            isMounted: function () {
              return !1
            },
            enqueueForceUpdate: function () {},
            enqueueReplaceState: function () {},
            enqueueSetState: function () {}
          },
          r = Object.assign,
          a = {}
        function n(t, e, r) {
          ;(this.props = t),
            (this.context = e),
            (this.refs = a),
            (this.updater = r || o)
        }
        function c() {}
        function p(t, e, r) {
          ;(this.props = t),
            (this.context = e),
            (this.refs = a),
            (this.updater = r || o)
        }
        ;(n.prototype.isReactComponent = {}),
          (n.prototype.setState = function (t, e) {
            if ('object' != typeof t && 'function' != typeof t && null != t)
              throw Error(
                'setState(...): takes an object of state variables to update or a function which returns an object of state variables.'
              )
            this.updater.enqueueSetState(this, t, e, 'setState')
          }),
          (n.prototype.forceUpdate = function (t) {
            this.updater.enqueueForceUpdate(this, t, 'forceUpdate')
          }),
          (c.prototype = n.prototype)
        var s = (p.prototype = new c())
        ;(s.constructor = p), r(s, n.prototype), (s.isPureReactComponent = !0)
        Array.isArray, Object.prototype.hasOwnProperty
      },
      294: (t, e, o) => {
        o(408)
      }
    },
    e = {}
  !(function o(r) {
    var a = e[r]
    if (void 0 !== a) return a.exports
    var n = (e[r] = { exports: {} })
    return t[r](n, n.exports, o), n.exports
  })(294)
})()
```

# Estrutura do React.js

Alterar arquivo 'public/index.html':

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Título</title>
  </head>
  <body>
    <div id="root"></div>
    <script src="../dist/bundle.js"></script>
  </body>
</html>
```

Alterar arquivo 'src/index.jsx':

```js
// src/index.js
import { render } from 'react-dom'
import { App } from './App'

render(<App />, document.getElementById('root'))
```

Alterar arquivo 'babel.config.js':

```js
module.exports = {
  presets: [
    '@babel/preset-env',
    [
      '@babel/preset-react',
      {
        runtime: 'automatic'
      }
    ]
  ]
}
```

Teste de funcionamento:
Comando no termnal:

```bash
npx webpack
```

Arir 'public/index.html' com Live Server. Se tiver um título "Test", está funcionando!

### Corrigindo 'WARNING' do 'npx webpack'

Alterar: arquivo 'webpack.config.js':

```js
const path = require('path')

module.exports = {
  mode: 'development',
  entry: path.resolve(__dirname, 'src', 'index.jsx'),
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  resolve: {
    extensions: ['.js', '.jsx']
  },
  module: {
    rules: [
      {
        test: /\.jsx$/,
        exclude: /node_modules/,
        use: 'babel-loader'
      }
    ]
  }
}
```
