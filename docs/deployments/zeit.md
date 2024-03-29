# Zeit Now

## Instalacion

Se debe tener Node.js previamente instalado

```
npm install -g now
```

## Archivo de Configuracion

elephantsql

o en el archivo now.json

"alias" : "alias.now.sh"

## Comandos

- `now`: Ejecuta el deploy (de todos los archivos de la carpeta donde se encuentra posicionado).
- `now <PATH_PROJECT>`: Ejecuta el deploy de todos los archivos de la carpeta indicada.
- `now -e NODE_ENV=production -e MONGODB_PASSWORD=@password`: Ejecuta un deploy con variables de entorno.

[https://joaquinaraujo.github.io/deploy-now/](https://joaquinaraujo.github.io/deploy-now/)

Si se presenta algun error, en la raiz del proyecto crear un archivo now.json con el siguiente contenido

```json
{
  "version": 1,
  "name": "{NOMBRE DE LA APP}",
  "type": "docker"
}
```

- pubsub = Nos sirve para tener una forma de comunicarnos cuando hacemos la parte de las suscripciones en real time.
- resolvers = Nos sirven para saber qué hacer en cada query o cada cambio que el navegador envía al API.
- squema = Le escribimos todo el esquema de datos que tiene nuestra aplicación, los datos que existen.
- server = Donde inicializamos el servidor, sincronizamos el modelo con la base de datos, creamos el servidor express y creamos todo lo que necesitamos para correr en producción.

```
now alias
```

ultimo deploy al alias definido en el now.json

## Uso

### Despliegue Simple

Por medio de la consola acceder a la carpeta del proyecto y digitar el siguiente comando.

```
now
```

Se desplegara el proyecto y nos retornara una URL la cual podremos utilizar para abrir en el navegador.

### Cambiar la URL Generada

Podemos cambiar la url generada realizando el siguiente comando o utilizando el archivo now.json con la opcion `alias`:

```
now alias <GENERATED_URL_BY_NOW> <CUSTOM_URL>.now.sh
```

### Eliminar instancias creadas

```
now rm {URL_GENERADA}
```

## Deployment

Para hacer deploy a una aplicación sea de Node.js o de un contenedor de Docker, se debe tener el archivo de configuracion de now. Ademas se debe definir lo siguiente.

- Aplicacion de Node:
  ```json
  {
    "type": "npm"
  }
  ```

- Contenedor de Docker
  ```json
  {
    "type": "docker"
  }
  ```

- Mostrar ultimos deploys: `now ls`
- Deploy desde Github: `now <USER>/<REPO>`

## Secrets y Variables de entorno

Las variables de entorno se pueden definir en el archivo `now.json` de la siguiente manera.

```json
"env" : {
  "KEY" : "VALUE"
}
```

sin embargo se pueden definir `secrets` para no tener esta configuracion al descubierto, para hacerlo se usa el siguiente comando para crear nuestros propios secrets.

```
now secrets add {VAR_NAME} "{VAR_VALUE}"
```

```json
"env" : {
  "KEY" : "@{VAR_NAME}"
}
```

## Ver codigo fuente y logs

Una vez desplegado, se puede ver el codigo y los logs del proyecto agregando despues de la url `\_src` para los archivos y `\_log` para los logs.

## Dominios

Para usar el dominio de Zeit (zeit.world) el cual sus DNS son gratuitos se debe realizar la siguiente configuracion:

- Ir a Custom DNS
- Agregar los DNS definidos en Zeit

Para definir un dominio

```
now alias <URL_GENERADA> <Custom Domain>
```

### Comprar dominios

```
now domain buy <URL>.com
```

## Componer microservicios

Archivo `rules.json`

```json
{
  "rules": [
    {
      "pathname": "/graphql",
      "dest": "[aplicacion].now.sh"
    },
    {
      "pathname": "/[ruta]",
      "dest": "[aplicacion].now.sh"
    },
    {
      "dest": "[aplicacion].now.sh"
    }
  ]
}
```

La forma de establecer esta configuración en Now.sh es por medio de el comando:

now alias [aplicacion].now.sh -r rules.json Permite establecer las configuraciones de rules.json en un deploy de Now.sh.

## Ayudas:

- [https://platzi.com/comentario/349139/](https://platzi.com/comentario/349139/)
- [https://github.com/platzi/now-course](https://github.com/platzi/now-course)
- [https://zeit.co/docs/](https://zeit.co/docs/)
- [https://platzi.com/comentario/331097/](https://platzi.com/comentario/331097/)