### VS code development frontend
- Settings - Editor: Tab Size - 2
- Shift + Alt + F - Format code

### Init project
```sh
npm create vue@latest
cd <your-project-name>
npm install
```

### Compile and Hot-Reload for Development
```sh
npm run dev
```

### Compile and Hot-Reload for Development
```sh
npm run server
```

### Compile and Minify for Production
```sh
npm run build
```

### Tailwind css install + configure
```sh
npm install -D tailwindcss@latest postcss@latest autoprefixer@latest
npx tailwindcss init -p
```

#### tailwind.config.js
- content: ['./index.html', './src/**/*.{vue,js,ts,jsx,tsx}'],
- add to assets/main.css + import in main.js
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```


### Prime Icons Vue
```sh
npm install primeicons
```
- add import 'primeicons/primeicons.css' -> main.js


### Vue router
- npm install vue-router

### Json server
- npm install json-server

### Axios
- npm install axios

### Vue spinner
- npm install vue-spinner

### Vue toasts
- npm i vue-toastification@next