# Prettier

## Install

```npm
npm install -D prettier
```

## Setup

### Config

```json title=".prettierrc"
{
    "printWidth": 100,
    "tabWidth": 4,
    "useTabs": false,
    "semi": true,
    "singleQuote": false,
    "trailingComma": "none",
    "bracketSpacing": true,
    "bracketSameLine": false,
    "arrowParens": "avoid",
    "htmlWhitespaceSensitivity": "ignore"
}
```

### Application

```json hl_lines="8 9"
{
    "scripts": {
        "ng": "ng",
        "start": "ng serve",
        "build": "ng build",
        "watch": "ng build --watch --configuration development",
        "test": "ng test",
        "format:test": "prettier --list-different \"./src/**/*.{ts,html,css,scss,json}\"", 
        "format:write": "prettier --write \"./src/**/*.{ts,html,css,scss,json}\""
    },
}
```

### Workspace Project

```json hl_lines="8 9"
{
    "scripts": {
        "ng": "ng",
        "start": "ng serve",
        "build": "ng build",
        "watch": "ng build --watch --configuration development",
        "test": "ng test",
        "format:test": "prettier --list-different \"./projects/**/*.{ts,html,css,scss,json}\"",
        "format:write": "prettier --write \"./projects/**/*.{ts,html,css,scss,json}\"",
    },
}
```
