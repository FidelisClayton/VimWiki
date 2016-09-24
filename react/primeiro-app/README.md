# Passo a passo

## 1 - Configurando o projeto

### 1.1 Estrutura de pastas
```
├── bin
│   └── app.bundle.js
├── index.js
├── package.json
├── src
│   ├── components
│   │   └── App.js
│   └── main.js
└── webpack.config.js
```

### 1.2 Dependências
* Dependências de desenvolvimento
    * [babel-core](https://github.com/babel/babel/tree/master/packages/babel-core)
    * [babel-loader](https://github.com/babel/babel-loader)
    * [babel-preset-es2015](https://github.com/babel/babel/tree/master/packages/babel-preset-es2015)
    * [babel-preset-react](https://github.com/babel/babel/tree/master/packages/babel-preset-react)
    * [webpack](https://github.com/webpack/webpack)
* Dependências do projeto
    * [react](https://github.com/facebook/react)
    * [react-dom](https://github.com/facebook/react/tree/master/packages/react-dom)

* Instalando dependências
    * Primeiramente vamos iniciar nosso arquivo **package.json**
    ```
    npm init -y
    ```
    * Em seguida as dependencias do projeto:
    ```
    npm install --save-dev babel-core babel-loader babel-preset-es2015 babel-preset-react webpack
    npm install --save react react-dom
    ```
    * Nosso arquivo **package.json** ficará assim:
    ```json
    {
      "name": "react-todo",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
      },
      "keywords": [],
      "author": "",
      "license": "ISC",
      "devDependencies": {
        "babel-core": "^6.14.0",
        "babel-loader": "^6.2.5",
        "babel-preset-es2015": "^6.14.0",
        "babel-preset-react": "^6.11.1",
        "webpack": "^1.13.2"
      },
      "dependencies": {
        "react": "^15.3.1",
        "react-dom": "^15.3.1"
      }
    }
    ```    

### 1.2 - Configurando o webpack
* Configurando o arquivo **.babelrc**
```json
    {
        "presets": [
            "es2015",
            "react"
        ]
    } 
```
* Configurando o arquivo **webpack.config.js**
```javascript
    var webpack = require('webpack');

    module.exports = {
        entry: './src/main.js', // Arquivo principal da aplicação
        output: {
            path: './', // Pasta onde ficará o pacote gerado pelo webpack
            filename: 'app.bundle.js' // Nome do pacote gerado pelo webpack
        },
        module: {
            loaders: [
                {
                    test: /.jsx?$/, // Verifica se o arquivo possui a extensão .jsx
                    loader: 'babel-loader', // Loader responsável por converter JS ES6 para ES5
                    exclude: /node_modules/, // Evita que o webpack leia os arquivos da pasta node_modules
                }
            ]
        }
    };
```

## 2 - Criando nosso primeiro Component
### 2.1 - O que são Components?
Components são pequenos "pedaços" da nossa aplicação que podem ser utilizados várias e várias vezes dentro dela (ou até mesmo fora).
<Bota uma imagem mostrando a componentização de uma tela>
    
### 2.2 - Mão na massa!
Primeiro vamos criar o arquivo **index.html**, nele adicionaremos a **div#app** que é onde nossa aplicação será renderizada e por último importamos o script
**app.bundle.js** gerado pelo **webpack**.

```html
    <!DOCTYPE html>
    <html>
    <head>
        <meta charset="UTF-8">
        <title>React APP</title>
    </head>
    <body>
        <h1>React rocks!</h1>
        <div id="app"></div>
        
        <script src="app.bundle.js"></script>
    </body>
    </html>
```

Agora vamos criar o arquivo **main.js** que será responsável por renderizar a aplicação na div que adicionamos no html.
```javascript
    // src/main.js
    import React from 'react';
    import { render } from 'react-dom';
    
    render(
        <h1> Hello World! </h1>, 
        document.getElementById("app")
    );
```

Em seguida executamos o webpack para que ele possa gerar nosso **bundle**:
```
    > webpack
    
    Hash: 484a034e635dcd78a455
    Version: webpack 1.13.2
    Time: 980ms
            Asset    Size  Chunks             Chunk Names
    app.bundle.js  738 kB       0  [emitted]  main
        + 172 hidden modules

```

Agora é só abrir o arquivo *index.html* no browser. Et voilá!

### 2.3 - HelloWorld Component

Legal, mas ainda não criei nenhum Component, e agora? Vamos lá!
Nosso componente HelloWorld vai herdar a classe **Component** do **React** e em seguida
definimos o método **render** retornando o que queremos que o **Component** renderize.

```javascript
import React, { Component } from 'react'; // Importamos o React e o Component

// Agora é só extender a classe Component para nosso HelloWorldComponent
export default class HelloWorld extends Component {
    render() {
        return (
            <h1>Hello World Component!!</h1>
        );
    }
}
```
Component criado agora é só importá-lo no nosso **main.js** e utilizá-lo.

```javascript
    // src/main.js
    import React from 'react';
    import { render } from 'react-dom';

    import HelloWorld from './components/HelloWorld';
    
    render(
        <HelloWorld />, 
        document.getElementById("app")
    );
```

Novamente rodamos o comando **webpack** no console e atualizamos a página. *SHAZAM C@%$&!!!!*

## 3 - Estilizando nosso Component

**Legal, mas tá feio...** Vamos lá!

### 3.1 - Inline Styles
A primeira forma de aplicar estilos que veremos é o **Inline Styles**, onde definimos um objeto
javascript com os atributos de estilos, em seguida passamos a váriavel de estilos para o Virtual DOM.

```javascript
export default class HelloWorld extends Component {
    render() {
        let styles = {
            color: '#98d8b0',
            fontSize: '65px',
            fontWeight: 'normal',
            lineHeight: '60px',
            margin: '10px 0 20px',
            textTransform: 'uppercase',
            textAlign: 'center',
            width: '450px',
            margin: '0 auto'
        };        

        return (
            <h1 style={ styles }>Hello World Component!!</h1>
        );
    }
}
```
Continua feio, mas deu pra entender como funciona.

### 3.2 - Bom e velho CSS
Para esse exemplo vamos importar o CSS do bootstrap, para isso precisaremos baixar o bootstrap e mais algumns loaders para o webpack.

[TODO]

## 4 - Props, States e Refs

[TODO]

## 5 - Instalando um servidor de desenvolvimento
### 5.1 - Dependências
* Dependencias globais
    * [webpack-dev-server](https://github.com/webpack/webpack-dev-server)

* Instalando o **webpack-dev-server**
```
> npm install webpack-dev-server -g
```

### 5.2 - Iniciando o servidor
Já instalamos o servidor, agora só precisamos inicializá-lo. Basta executar o comando *webpack-dev-server*
no terminal.
```
> webpack-dev-server
```

Em seguida basta acessar o endereço *http://localhost:8080* no navegador para visualizar a aplicação.

Agora vamos habilitar o **livereloading** no **webpack-dev-server** adicionando o seguinte trecho no final
do arquivos **webpack.config.js**.

```javascript
     plugins: [                                                          
        new webpack.HotModuleReplacementPlugin() 
     ],                                                                  
     devServer: {                                                        
        hot: true, // Ativa o HotModuleReplacement
        inline: true // Inicia o server no modo inline                        
     }  
```
Em seguida iniciamos o **webpack-dev-server** novamente e acessamos o endereço *http://localhost:8080*, agora
a página irá atualizar sempre que fizermos algumas alteração no código da nossa aplicação.