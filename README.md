# Teil 3 - Nappl-Login 

Was lerne ich in diesem Teil? 
* Per nodejs fürgen wir das Paket `axios` hinzu, um dem Benutzer unserer App mit Hilfe dessen den Login zu ermöglichen. Dazu nutzen wir die GraphQL-Schnittstelle des Application Layer.

<br/>

## Und los gehts...
1. Wie angedroht installieren wir als erstes das npm-Modul `axios`.
```
npm i axios
```

2. TODO

3. TODO

4. TODO

5. Bevor unsere Vue-App aus dem Browser heraus direkt mit der GraphQL-Schnittstelle des Application Layer sprechen kann, müssen wir unseren Development-Webserver etwas konfigurieren. Die Same-Origin-Policy (SOP) verbietet beim Besuch einer Website das Nachladen von anderen Servern. Alle Daten sollen von der gleichen Quelle kommen, also dem gleichen Server entspringen. Das ist eine Sicherheitsmaßnahme. 
Deshalb richten wir einen Proxy ein, welcher bestimmte Anfragen an den Application Layer weiterleitet. Dazu ergänzen wir die Datei `vite.config.ts` wie folgt.
```javascript
/* vite.config.ts */ 
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vitejs.dev/config/
export default defineConfig({
  server: {
    proxy: {
      "/api": {
        target: "http://localhost:8080",
        changeOrigin: true,
        secure: false,
        rewrite: (path) => path.replace(/^\/api/, ""),
      },
    },
  },
  plugins: [vue()]
})
```
So können wir dann im Browser GraphQL-Anfragen über den gleichen Host und Port absetzten. `http://localhost:3000/api/nscalealinst1/graphql`

