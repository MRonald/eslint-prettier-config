# Configurar ESLint e o Prettier no React Native Com Typescript

## Primeiros passos

1. `npm uninstall @react-native-community/eslint-config` - React Native já vem com o Eslint inicial quando criamos o projeto mas vamos remover esse pacote porque criaremos a nossa configuração.

2. `npm uninstall eslint` - Agora removeremos o eslint.

3. Provavelmente já vai vir no seu projeto criado um arquivo com nome de `.eslintrc` você pode Excluir esse arquivo.

4. Você também já vai ter um arquivo chamado `.prettierrc` você pode Excluir esse arquivo.

5. `npm install eslint --save-dev` - Agora vamos instalar o `eslint`

6. `npx eslint --init` - Vamos iniciar nossa configuração. Este comando fará algumas perguntas via CMD. Aqui está uma lista delas e as respostas que precisaremos escolher (`✔` and `❯` os símbolos indicam as respostas selecionadas):

```bash
# pergunta 1:
? How would you like to use ESLint? …
   To check syntax only
   To check syntax and find problems
❯❯ To check syntax, find problems, and enforce code style

# pergunta 2:
? What type of modules does your project use? …
❯❯ JavaScript modules (import/export)
   CommonJS (require/exports)
   None of these

# pergunta 3:
? Which framework does your project use? …
❯❯ React
   Vue.js
   None of these

# pergunta 4 (selecione "Yes"):
? Does your project use TypeScript? ❯ No / Yes

# pergunta 5: Aqui vai vir com ambos selecionados você pode apertar ESPAÇO do seu teclado para selecionar ou desmarcar uma opção do cmd.
? Where does your code run? …
   Browser
 ✔ Node

# question 6:
? How would you like to define a style for your project? …
❯❯ Use a popular style guide
   Answer questions about your style
   Inspect your JavaScript file(s)

# question 7 (Vamos usar o padrao do Airbnb):
? Which style guide do you want to follow? …
❯❯ Standard: https://github.com/standard/eslint-config-standard-with-typescript
   XO: https://github.com/xojs/eslint-config-xo-typescript

# question 8:
? What format do you want your config file to be in? …
   JavaScript
   YAML
❯❯ JSON

# O cmd final aqui é onde o eslint perguntará se você deseja instalar todas as dependências necessárias. Selecione "YES" e pressione enter:
Checking peerDependencies of eslint-config-airbnb@latest
The config that you have selected requires the following dependencies:

eslint-plugin-react@^7.21.5 eslint-config-airbnb@latest eslint@^5.16.0 || ^6.8.0 || ^7.2.0 eslint-plugin-import@^2.22.1 eslint-plugin-jsx-a11y@^6.4.1 eslint-plugin-react-hooks@^4 || ^3 || ^2.3.0 || ^1.7.0

? Would you like to install them now with npm? › No / ❯ Yes
```

Como resultado, você acabará tendo um `.eslintrc.json` arquivo na raiz do seu projeto, modifique para que ele tenha a seguinte estrutura:

```json
{
  "env": {
    "es2021": true,
    "node": true
  },
  "extends": [
    "standard-with-typescript",
    "plugin:react/recommended",
    "prettier",
    "plugin:@typescript-eslint/recommended",
    "prettier/@typescript-eslint",
    "plugin:prettier/recommended"
  ],
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module"
  },
  "plugins": ["react", "react-native", "@typescript-eslint"],
  "rules": {
    "react/jsx-filename-extension": [1, { "extensions": [".ts", ".tsx"] }],
    "no-use-before-define": ["error", { "variables": false }],
    "react/prop-types": [
      "error",
      { "ignore": ["navigation", "navigation.navigate"] }
    ],
    "react/react-in-jsx-scope": "off"
  }
}
```

7. Agora instale: `npm install --save-dev eslint-plugin-react-native`

8. Crie na raiz do seu projeto um arquivo chamado `.eslintignore` para dizer ao ESLint para ignorar arquivos e diretórios específicos e, em seguida, adicione o seguinte conteúdo neste arquivo:

```bash
node_modules/
android/
ios/
.expo/
build/
logs/
assets/
```

9. A última etapa aqui é configurar seu editor de código para fazer o lint do código ao salvar o arquivo.

- Vá na aba extenções e procure por [**Eslint**](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) clique e instale ela.

- Depois vamos ativar no vscode para fazer o fix quando salvar o seu código, no seu VsCode aperte as teclas `Control + Shift + P` e procure **User Settings (JSON)**
- [Clique aqui para acessar o exemplo](https://prnt.sc/Pb77K8PeF2xh)

- Agora vamos adicionar essa configuração:

```json
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```

## Instalando e configurando o Prettier

1. Rode: `npm install --save-dev --save-exact prettier`

2. Depois de instalar vá até as extensoes do seu VSCode e procure por [**Prettier**](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) e instale.

3. Agora rode no cmd novamente: `npm install --save-dev eslint-config-prettier` - usaremos o Prettier para questões de formatação de código e ESLint para questões de qualidade de código, portanto, precisamos desativar todas as regras ESLint que são desnecessárias ou podem entrar em conflito com o Prettier.

4. Agora **crie na raiz do seu projeto** um arquivo chamado `.prettierrc.json` e nele podemos passar algumas configurações:

```json
{
  "arrowParens": "always",
  "bracketSpacing": true,
  "jsxBracketSameLine": false,
  "jsxSingleQuote": false,
  "quoteProps": "as-needed",
  "singleQuote": true,
  "semi": true,
  "printWidth": 100,
  "useTabs": false,
  "tabWidth": 4,
  "trailingComma": "es5"
}
```

- Exemplo configurações falando para usar espaço, quantos espaços ele aplicar ao usar o tab, para usar aspas simples ao invés de aspas duplas.

Pode depois conferir toda documentaçãao aqui: [Prettier Documentation](https://prettier.io/docs/en/options.html).

5. E agora para funcionar todo prettier corretamente volte a configuração do seu VsCode, novamente aperte `Control + Shift + P` e procure **User Settings (JSON)**

- [Clique aqui para acessar o exemplo](https://prnt.sc/Pb77K8PeF2xh)

**E adicione mais essa configuração: 👇**

```json
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true
}
```

- [Clique aqui para acessar o exemplo como ficou](https://prnt.sc/ar2Num7hiBlo)

6. Para finalizar crie o arquivo `.prettierignore` na raiz do seu projeto e adicione o seguinte conteúdo:

```bash
node_modules/
android/
ios/
.expo/
build/
logs/
assets/
```
