# NodeJs

### EXPRESS JS

- node app.js OR nodemon app.js
    * start server
    * localhost:4000

* npm run dev 
    * à la place de "nodemon app.js"
    ```js package.json
    "scripts": {
        "dev": "nodemon ./src/app.js"
    },
    ```

* type module 
    ```js  
    // package.json
        {
            "type": "module",
        }

    // ex app.js ou autre fichier
        import {} from "dotenv/config"; 
        // à la place de
        const dotenv = require('dotenv')
        dotenv.config()
    ```

- npm i express

- npm i dotenv
    
    * fichier .env  // variables de environement (caches)
    * process.env.NAME_VARIABLE

- npm i cors

    * ```js
        const dotenv = require('dotenv')

        dotenv.
      ```

- npm i nodemon -D 
    * seulement pour le developpement 
    ```js package.json
    "devDependencies": {
        "nodemon": "^3.1.4"
    }
    ```

