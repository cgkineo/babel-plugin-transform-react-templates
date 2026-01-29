# babel-plugin-transform-react-templates

> Register react templates with a global function

## Install

Using npm:

```sh
npm install --save-dev babel-plugin-transform-react-templates
```

or using yarn:

```sh
yarn add babel-plugin-transform-react-templates --dev
```

## Usage

Code:

```js
// src/reactTemplateHelpers.js
export default function register(template, component) {
  templates[template] = component;
}

export const templates = {};
```

```js
// src/templates/test.jsx
export default (data) => {
  return <div className="test">
    {data.testText}
  </div>
}
```

```js
// src/main.js
import { templates } from 'src/reactTemplateHelpers';

ReactDOM.render(templates['test']({
  testText: 'testing text'
}), '#app');

```

With options:

```js
plugins: [
  [
    'transform-react-templates',
    {
      includes: [
        // Any jsx file nested inside a templates folder
        '**/templates/**/*.jsx'
      ],
      importRegisterFunctionFromModule: 'src/reactTemplateHelpers.js',
      registerFunctionName: 'register',
      registerTemplateName: (moduleId) => {
        // Use filename as template name
        return path.parse(moduleId).name;
      }
    }
  ]
]
```

Notes:
You must inject the template paths if you want them to appear automatically or include them in a normal import.
