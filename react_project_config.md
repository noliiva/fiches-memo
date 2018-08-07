# Config for React projects
Principaly started with create-react-app.

## package.json
```
"scripts": {
  "precommit": "lint-staged",
  "prettier": "prettier --log-level=debug --write 'src/**/*.{js,jsx,json,css,scss}'",
  "extract-intl": "babel-node --presets env -- scripts/extract-intl.js",
  "lint": "eslint src/**/*.{js,jsx} --quiet",
},
"lint-staged": {
  "src/**/i18n.js": [
    "npm run extract-intl",
    "git add **/src/i18n/*.json"
  ],
  "src/**/*.{js,jsx,css,scss}": [
    "npm run prettier",
    "git add",
    "npm run lint"
  ]
},
```

## .eslintrc
```
{
    "extends": ["react-app", "prettier"],
    "rules": {
        "no-unused-vars": ["error"]
    }
}
```

## .prettierrc
```
{
    "arrowParens": "avoid",
    "bracketSpacing": true,
    "jsxBracketSameLine": true,
    "parser": "babylon",
    "printWidth": 100,
    "semi": true,
    "singleQuote": true,
    "tabWidth": 4,
    "trailingComma": "none",
    "useTabs": false
}
```
