# Prettier

## Install

```npm
npm install -D prettier
```

## Setup

### Single App

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

### Workspace

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
