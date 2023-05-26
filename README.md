# Typescript Start Project

## 🚧 Under construction

The idea of this project is help you to start with a simple typescript project including some configurations for to your codebase syntax and style as:

- Linting
- Formatting
- Type Checking

## Getting started

### Compiling Typescript code

#### Typescript

Typescript is a superset of Javascript that help us with static type checking at compile time.

First we neet a compiler to run Typescript code into Javascript:

```sh
npm install --save-dev typescript
```

Create an `index.ts` file in the `src` directory:

```typescript
const favoriteFruits: string[] = ["apple", "strawberry", "orange"];

function addFruit(fruit) {
  favoriteFruits.push(fruit);
}
```

Compile the code

```sh
npx tsc src/index.ts

```

Create a typescript compiler settings to your project:

```sh
npx ts``c --init
```

Modify the file `tsconfig.json` to:

```json
// tsconfig.json
{
  "compilerOptions": {
    "outDir": "dist", // where to put the compiled JS files
    "target": "ES2020", // which level of JS support to target
    "module": "CommonJS", // which system for the program AMD, UMD, System, CommonJS

    // Recommended: Compiler complains about expressions implicitly typed as 'any'
    "noImplicitAny": true
  },
  "include": ["src"], // which files to compile
  "exclude": ["node_modules"] // which files to skip
}
```

Include a command into your `package.json`:

```json
// package.json
{
  "name": "Linting TypeScript with ESLint",
  "version": "1.0.0",
  "devDependencies": {
    "typescript": "^4.9.4"
  },
  "scripts": {
    "dev": "tsc --watch"
  }
}
```

#### ESLINT

A tool for linting wich will analyze your code to find potential bugs and improve your code quality by defining coding conventions and then automatically enforcing them.

Install the following dependencies to your `devDependecies`:

```sh
npm install eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin --save-dev
```

- `eslint`: ESLint core library
- `@typescript-eslint/parser`: a parser that allows ESLint to understand TypeScript code
- `@typescript-eslint/eslint-plugin`: plugin with a set of recommended TypeScript rules

Similar to Typescript compiler settings, you can either use the command line to generate a configuration file using the --init flag from ESLint or create it manually. Either way, it’s mandatory to have your ESLint configuration file.

Let’s create a configuration file using the CLI. Run the following command in the terminal:

```sh
npx eslint --init
```

Next, you will see a series of questions that allow you to adjust the configuration file based on your preferences:

- How would you like to use ESLint?
- What type of modules does your project use?
- Which framework does your project use?
- Does your project use TypeScript?
- Where does your code run?
- How would you like to define a style for your project?

Based on the options selected, the ESLint CLI will create a .eslintrc.json configuration file in the project’s root directory with some default settings. If you already have your favorite settings, you can replace some of the options in the configuration file.

You can also explore the full list of [ESLint settings available](https://eslint.org/docs/latest/user-guide/configuring/) for the configuration file.

### Linting with ESLint

For this article, replace the default settings in the configuration file with this:

```json
// .eslintrc
{
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaVersion": 12,
    "sourceType": "module"
  },
  "plugins": ["@typescript-eslint"],
  "extends": ["eslint:recommended", "plugin:@typescript-eslint/recommended"],
  "rules": {},
  "env": {
    "browser": true,
    "es2021": true
  }
}
```

- parser: this specifies a parser for ESLint to use when analyzing the code
- parserOptions: specifies what JS language options you want to support, such as the version of ECMAScript syntax you want to use
- plugins: this is where you define plugins to use
- extends: tells ESLint what configuration is set to extend from. The order matters, as the last extend option will override the previous ones in any conflicting configurations.
- env: which environments your code will run in

When we add an ESLint rule, it overrides the configuration defined in the extends list. Let’s add a couple of rules to see how it works:

```json
// .eslintrc
{
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaVersion": 12,
    "sourceType": "module",
  },
  "plugins": ["@typescript-eslint"],
  "extends": ["eslint:recommended", "plugin:@typescript-eslint/recommended"],

  "rules": {
    "@typescript-eslint/no-unused-vars": "error",
    // to enforce using type for object type definitions, can be type or interface
    "@typescript-eslint/consistent-type-definitions": ["error", "type"],
  },

  "env": {
    "browser": true,
    "es2021": true
  }
}

---

Made by Fernando Alves [See my linkedIn][socialIn]
```
