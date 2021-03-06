# Backend escalable
Buenas practicas de una estructura básica y escalable de un backend

## Tabla de contenido
- [Preparando ENTORNO con BUENAS PRACTICAS](#preparando-entorno-con-buenas-prácticas)
- [Creando SERVIDOR del proyecto con EXPRESS](#creando-servidor-del-proyecto-con-express)


## Preparando entorno con buenas prácticas

1. Crear la carpeta del proyecto en la ubicación deseada de tu equipo local.

2. Inicializar configuración dentro de la carpeta del proyecto con el siguiente comando desde la terminal:
```bash
npm init -y
```

3. Inicializar repositorio git con el siguiente comando:
```bash
git init
```

4. Crear los archivos de configuración iniciales, recomendados como buena practica.  Se pueden crear con el siguiente comando:
```bash
touch .gitignore .editorconfig .eslintrc.json .prettierrc.json
```

* `.gitignore` Para Indicar los archivos y/o carpetas que el repositorio git ignorará.  
    1. El contenido a pegar en este archivo se encuentra en https://www.toptal.com/developers/gitignore/ 
    2. Debe escribir en la barra central de la pagina y seleccionar  una por una las palabras claves para configurar un entorno que ignore lo que deseamos. Ej: node, windows, linux, macOs
    3. Dar click en Create 
    4. Y por ultimo copiar y pegar el contenido generado.

* `.editorconfig` Para las configuraciones del editor.
    1. Tener instalada en Visual Studio Code la extensión: 
    ```bash
    EditorConfig for VS Code
    ```
    2. Copiar y pegar el contenido de configuración inicial que se encuentra en https://editorconfig.org/

* `.eslintrc.json` Para las reglas de buenas prácticas del código.
    1.  Copiar y pegar el contenido que se encuentra en https://github.com/T-percy/contenido-slintrc.json

* `.prettierrc.json` Para que nuestro código y el de los demas desarrolladores tengan el mismo formato al hacer commit.
    
5. Crear los scripts del package.json para los entornos de desarrollo y producción:
    Opción 1
    ```bash
    "dev": "nodemon src/server.js",
    "start": "node src/server.js",
    "lint": "eslint"
    ```
    Opción 2
    ```bash
    "dev": "DEBUG=app:* nodemon src/server.js",
    "start": "NODE_ENV=production node src/server.js",
    "lint": "eslint"
    ```

6. Instalar las dependencias de desarrollo necesarias, por ejemplo:
    ```bash
    npm i nodemon eslint eslint-config-prettier eslint-plugin-prettier prettier -D
    ```

7. Crear carpeta src y dentro de ella el archivo de arranque del servidor:
    `server.js` ó `index.js`

8. Probar que corran correctamente los entornos de desarrollo y producción.
    1. Imprimir un console.log en el archivo de arranque del servidor con cualquier mensaje.
    2. En la terminal ejecutar los siguientes comandos por separado:
    ```bash
    npm run dev
    ```
    ```bash
    npm start
    ```

9. Guardar proyecto en el repositorio local con los siguientes comandos: 
    1. `git status`, 
    2. `git add .`, 
    3. `git commit -m "Mensaje que identifique lo que acaba de guardar"`

10. Subir proyecto al repositorio remoto (github):
    Para el primer push, ejecutar los siguientes comandos, uno por uno:
    ```bash
    git remote add origin url
    ```
    ```bash
    git branch -M main
    ```
    ```bash
    git push -u origin main
    ```

    Desde el segundo push en adelante con el siguiente comando es suficiente:
    ```bash
    git push
    ```

## Creando servidor del proyecto con express

1. Instalar express y/o todas las dependencias requeridas para el proyecto como por ej:
    ```bash
    npm i express mysql validator dotenv cors morgan body-parser bcrypt-nodejs connect-multiparty just-simple moment mongoose mongoose-paginate-v2
    ```

    * ### Proposito de las dependencias relacionadas
    `express` Para crear el servidor.
    `mysql` 
    `mongoose` Para manejar base de datos en mongoDB.
    `mongoose-paginate-v2` Para listar y paginar la información.
    `validator` Para validar datos, emails, strings, números...
    `dotenv` Para configurar las variables de entorno.
    `cors` Para permitir las conexiones de los clientes a nuestro backend.
    `morgan` Para ver las peticiones que está recibiendo nuestro servidor en tiempo real.
    `body-parser` Para traducir todo lo que nos manda cliente al formato JSON.
    `bcrypt-nodejs` Para las contraseñas.
    `connect-multiparty` Para subir archivos al backend.
    `just-simple` (autenticación) Para generar token al usuario que irá con la petición, el backend comprobará que sea el correcto para dar el permiso.
    `moment` Para procesar fechas.

2. Para que el código haga el formateo automatico cada vez que un desarrollador haga commit en el local y push para subirlo al repositorio se debe instalar el siguiente hook:
```bash
npx mrm lint-staged
```

3. Desde el archivo principal del servidor importar el modulo express `const express = require('express');` y todas las librerias necesarias.

4. Crear el objeto de la aplicación y guardarle la funcion express `const app = express();`.

5. Definir los middlewares de la app, por ej: `app.get('/', (req, res) => { res.send(200)});`.

6. Llamar al puerto por dónde escuchará el servidor:
    * Crear la variable del puerto `const port = process.env.PORT || 3000;`.
    * Poner a escuchar al servidor `app.listen(port, () => {});`.

--------------------