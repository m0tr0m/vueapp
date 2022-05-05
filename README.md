# Teil 1 - Einführung 
> Das Ergebnis des Workshops ist in Github zu finden https://github.com/m0tr0m/vueapp.git

Was lerne ich in diesem Teil? 
* Wir setzen gemeinsam eine Vue3-HelloWorld-App mit Hilfe des Build-Tools [vite](https://vitejs.dev/) auf. Unser Projekt soll Typescript unterstützten. Für's Auge werden wir das CSS-Framework [tailwindcss](https://tailwindcss.com/) in unser Projekt einbinden. 

<br/>

### Was brauche ich?
* Aktuelle `node.js` Installation [Download hier](https://nodejs.org/en/download/)
* Entweder `Visual Studio Code`, `Webstorm` oder natürlich `Intellij Ultimate`

<br/>

### Wichtige Links
* [Getting Started with Vite](https://vitejs.dev/guide/)
* [Getting Started with tailwindcss and Vite](https://tailwindcss.com/docs/guides/vite)

<br/>

## Und los gehts...
1. Als erstes lassen wir nodejs per Kommandozeile ein Vue3-Projekt inkl. Typescript anlegen, welches das Build-Tool `vite` verwendet.
```
npm create vite@latest vueapp -- --template vue-ts
```

2. Jetzt laufen wir in den zuvor neu angelegten Ordner.
```
cd vueapp
```

3. Dann initialisieren wir das durch den ersten Schritt angelegte Node-Js Projekt.
```
npm i
```

4. Zusätzlich installieren wir das Tailwind-CSS-Framework und die dazu gehörigen Abhängigkeiten.
```
npm i -D tailwindcss postcss autoprefixer
```

5. Nun initialisieren wir noch die für Tailwind-CSS nötigen Konfigurations-Dateien. Vorher muss du evtl. `npm` installieren. Das tun wir global über den ersten Befehl (`npx` ist quasi das `npm`-Equivalent für binäre Pakete).
```
npm install -g npx
npx tailwindcss init -p
```

6. Wir ändern den Eintrag `content` der Datei `tailwind.config.js` wie folgt, um dem CSS-Preprozessor (PostCSS) die Vuejs speuifischen Template-, die Javascript- und Typescript-Dateien bekannt zu machen.
```javascript
/* tailwind.config.js */
module.exports = {
  content: [
    "./index.html",
    "./src/**/*.{vue,js,ts}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

7. Wir legen die Datei `index.css` im Root-Verzeichnis unseres Projekts mit folgendem Inhalt an. Über die `@tailwind`-Direktiven sorgen wir dafür, dass die augeführten Tailwind-Standard-Layer geladen werden, sobald die `index.css` innerhalb unseres Projekts import wird.
```css
/* index.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
``` 

8. Nun importieren wir die zuvor angelegte `index.css` in der Datei `main.ts`. Die Datei sieht dann so aus:
```typescript
/* main.ts */
import { createApp } from 'vue'
import App from './App.vue'
import './index.css'

createApp(App).mount('#app')
```

9. Jetzt können wir die `HelloWorld.vue` öffnen und etwas abändern.
```javascript
/* HelloWorld.vue */
<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ msg: string }>()

const count = ref(0)
</script>

<template>

  <div class="flex w-full h-full justify-center items-center">
    <h1 class="dark-world">{{msg}}</h1>
  </div>

</template>

<style scoped>
</style>
```

10. Zu guter letzt geben wir folgenden Befehl in die Komandozeile ein, damit nodejs einen lokalen Web-Server für die Entwicklung startet, welcher unsere App über http://localhost:3000 erreichbar macht. Änderungen werden damit sofort im Browser sichtbar.
```
npm run dev
```

## ...Und weiter gehts im Branch `Teil1`
