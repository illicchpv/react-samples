познакомлю с самопальным 'state manager' основанном на работе с URL. с хеш частью URL

---
'state manager', 'props drilling', nuqs, useState, window.history.pushState, window.history.replaceState 

---

например если в URL хранится счетчик и язык

http://localhost:5175/#count=29&lang=jp

то любой компонент приложения может эти параметры получить. вне зависимости от вложенности.
так что это наверно можно назвать глобальным хранилищем состояния приложения.
Такой подход тем более удобен тем что URL можно кому-то послать и тот перейдёт именно в нужное место программы.

Это маленький аналог https://www.npmjs.com/package/nuqs

---

## тут буду собирать всякие примеры и не очевидные случаи в REACT
---

[Website recoiljs: ](https://recoiljs.org)

---

- create minimal vite react project https://vite.dev/guide/  
```
	>npm create vite@latest -y . -- --template react
```  
-   cd test-app //там запускаем vscode	
- edit package.json  
```
  "scripts": {
    "dev": "vite",
    "devOpen": "vite --open",
    "build": "vite build --base=./ --emptyOutDir",
    "lint": "eslint .",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^19.0.0",
    "react-dom": "^19.0.0"
  },
  "devDependencies": {
    "@types/react": "^19.0.8",
    "@types/react-dom": "^19.0.3",
    "@vitejs/plugin-react": "^4.3.4",
    "globals": "^15.14.0",
    "vite": "^6.1.0"
  }
```    
- >npm i
- убираем лишнее:   
```
    src\assets\**  ??? может и не надо
    src\App.css  
```    
- обнуляем     src\index.css
- редактируем App.jsx  
```
	function App() {
	  return (<h1>Vite + React</h1>)
	}
	export default App
``` 
- создаём src\components и переносим туда App.jsx  
- исправляем в 	src\main.jsx  ссылку на App.jsx 
	import App from './components/App.jsx'
- >npm i modern-normalize  
и подключаем его одним из способов:
```
	в main.jsx  import 'modern-normalize' либо 
	в index.css @import 'node_modules/modern-normalize/modern-normalize.css'; либо 
	в index.css @import 'modern-normalize';

```
- в README.md отмечаем что было установлено
```
  >npm create vite@latest -y test-app -- --template react
  >npm i
  >npm i modern-normalize
  >git init
```

- устанавливаем git  
``` 
  git init 
```

- для переименования сборок js и css в vite.config.js
```
const APP_DATE = new Date().toISOString().split('T')[1].split(':')[0];
const APP_PREFIX = 'cell';
const APP_VERSION = new Date().toISOString().split('T')[0].replaceAll('-', '') + APP_DATE;

...

  build: {
    rollupOptions: {
      output: {
        assetFileNames: (assetInfo) => {
          return `assets/${APP_PREFIX}_${APP_VERSION}_ass_` + assetInfo.names;
        },
        entryFileNames: (entryInfo) => {
          return `assets/${APP_PREFIX}_${APP_VERSION}_ent_` + entryInfo.name + '.js';
        },
        chunkFileNames: (chunkInfo) => {
          return `assets/${APP_PREFIX}_${APP_VERSION}_chu_` + chunkInfo.name + '.js';
        },
      }
    },
  },
```  
  или 
```  
  build: {
    rollupOptions: {
      output: {
        entryFileNames: `assets/[name].js`,
        chunkFileNames: `assets/[name].js`,
        assetFileNames: `assets/[name].[ext]`
      }
    },  
  },
```
