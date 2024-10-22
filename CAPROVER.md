## configuration caprover deploy

* ### git 
    * git add .
    * git commit -m "comentaire ..."

* ### if build project:
    * fichier (captain-definition)
    ``` 
        {
            "schemaVersion": 2,
            "dockerfileLines": [
                "FROM socialengine/nginx-spa:latest", 
                "COPY ./dist /app", 
                "RUN chmod -R 777 /app"
            ]
        }
    ```

    * npm run build

    * IN TERMINAL: tar -cvf ./deploy.tar --exclude='*.map' ./captain-definition ./dist/*
        * (dist) if it's a name of build's folder

    *fichier (.gitignore)
    ```
        deploy.tar
    ```

    * IN TERMINAL: caprover deploy -t ./deploy.tar 


* ### else if not build project
    * fichier (captain-definition)
    ``` 
        {
            "schemaVersion": 2,
            "dockerfilePath": "./Dockerfile"
        }
    ```
    
    * fichier (Dockerfile)
    ``` 
    <!-- fichier (Dockerfile) -->

        FROM node:18-alpine

        WORKDIR /app

        COPY package.json package-lock.json ./

        RUN npm install

        COPY . .

        EXPOSE 8080

        CMD ["npm", "run", "dev", "--host"]
    ```

    * fichier (package.json)
    ``` 
        "scripts": {
            "dev": "vite --host",
        },
    ```

    * fichier (vite.config.js)
    ``` 
        import { defineConfig } from 'vite'
        import react from '@vitejs/plugin-react-swc'

        // https://vitejs.dev/config/
        export default defineConfig({
            plugins: [react()],
            server: {
                port: 8080,
            },
        })

        <!--
            important !!! 
            server: {
                port: 8080,
            }, 
        -->
    ```

    * IN TERMINAL: caprover deploy