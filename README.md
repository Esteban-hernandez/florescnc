[![Deploy with Vercel](https://vercel.com/esteban-hernandez/florescnc)
# Flores cnc 

El kit de inicio todo en uno para sitios de comercio electrónico de alto rendimiento. Con unos pocos clics, los desarrolladores de Next.js pueden clonar, implementar y personalizar completamente su propia tienda. Comienza ahora mismo en [nextjs.org/commerce](https://nextjs.org/commerce)

Demostración en vivo en: [dev.florescnc.com](https://dev.florescnc.com)

- Shopify Demo: https://shopify.vercel.store/
- Swell Demo: https://swell.vercel.store/
- BigCommerce Demo: https://bigcommerce.vercel.store/
- Vendure Demo: https://vendure.vercel.store
- Saleor Demo: https://saleor.vercel.store/
- Ordercloud Demo: https://ordercloud.vercel.store/
- Spree Demo: https://spree.vercel.store/
- Kibo Commerce Demo: https://kibocommerce.vercel.store/
- Commerce.js Demo: https://commercejs.vercel.store/
- SalesForce Cloud Commerce Demo: https://salesforce-cloud-commerce.vercel.store/

## Ejecute la versión mínima localmente

> Para ejecutar una versión mínima de Next.js Commerce, puede comenzar con el proveedor local predeterminado `@vercel/commerce-local` que ha deshabilitado todas las funciones (carrito, autenticación) y usar archivos estáticos para el backend
```bash
yarn # Ejecute este comando en la carpeta raíz del repositorio mono
yarn dev
```

> Si encuentra algún problema durante la instalación y ejecución por primera vez, consulte la sección Solución de problemas
## Características

- Rendimiento por defecto 
- Listo para SEO 
- Internacionalización 
- Responsive 
- Componentes de la interfaz de usuario 
- Temas - Enlaces de datos estandarizados 
- Integraciones 
- Integración perfecta con las plataformas de comercio electrónico más comunes. 
- Soporte de modo oscuro

## integraciones

Next.js Commerce se integra de forma inmediata con BigCommerce, Shopify, Swell, Saleor, Vendure, Spree y Commerce.js. Planeamos admitir todos los principales backends de comercio electrónico.

## Consideraciones

- `packages/commerce` contiene todos los tipos, ayudantes y funciones que se utilizarán como base para construir un nuevo **proveedor**. 
- **provider** viven en la carpeta raíz de `packages` y ampliarán los tipos y la funcionalidad de Next.js Commerce (`packages/commerce`). 
- Tenemos una **API de funciones** para garantizar la paridad de funciones entre la interfaz de usuario y el proveedor. La interfaz de usuario debe actualizarse en consecuencia y no debe incluirse ningún código adicional. Toda la configuración adicional para las funciones se encontrará en `características` en `commerce.config.json` y, si es necesario, también se puede acceder mediante programación. 
- Cada **provider** debe agregar su correspondiente `next.config.js` y `commerce.config.json` agregando datos específicos relacionados con el proveedor. Por ejemplo, en el caso de BigCommerce, las imágenes CDN y las rutas API adicionales.


## Configuration

### Cómo cambiar de proveedor

Abra `site/.env.local` y cambie el valor de `COMMERCE_PROVIDER` al proveedor que le gustaría usar, luego configure las variables de entorno para ese proveedor (use `site/.env.template` como base).

La configuración de Shopify se vería así, por ejemplo
```
COMMERCE_PROVIDER=@vercel/commerce-shopify
NEXT_PUBLIC_SHOPIFY_STOREFRONT_ACCESS_TOKEN=xxxxxxxxxxxxxxxxxxxxxxxxxxxx
NEXT_PUBLIC_SHOPIFY_STORE_DOMAIN=xxxxxxx.myshopify.com
```

### Funciones

Cada proveedor define las funciones que admite en `packages/{provider}/src/commerce.config.json

#### Funciones disponibles 

Las siguientes funciones se pueden habilitar o deshabilitar. Esto significa que la interfaz de usuario eliminará todo el código relacionado con la función. 

Por ejemplo: Apagar `cart` deshabilitará las capacidades del carrito. 

- carrito 
- búsqueda 
- lista de deseos 
- customerAuth 
- customCheckout 

#### Cómo activar y desactivar las funciones

> NOTA: El proveedor seleccionado debe ser compatible con la función que está alternando. (Esto significa que no puede activar la lista de deseos si el proveedor no admite esta funcionalidad desde el primer momento)

- Abra `site/commerce.config.json`
- Verás un archivo de configuración como este:
  ```json
  {
    "features": {
      "wishlist": false,
      "customCheckout": true
    }
  }
  ```
- Active la "lista de deseos" configurando "wishlist" en "true".
- Ejecute la aplicación y la funcionalidad de la lista de deseos debería volver a estar activada.

### Cómo crear un nuevo proveedor

Siga nuestros documentos para [agregar un nuevo proveedor de comercio](packages/commerce/new-provider.md).

Si logró crear un proveedor, envíe un PR con una demostración válida y lo revisaremos lo antes posible.

## Contribuir

Nuestro compromiso con el código abierto se puede encontrar [aquí] (https://vercel.com/oss).

1. [Fork](https://help.github.com/articles/fork-a-repo/) this repository to your own GitHub account and then [clone](https://help.github.com/articles/cloning-a-repository/) it to your local device.
2. Create a new branch `git checkout -b MY_BRANCH_NAME`
3. Install the dependencies: `yarn`
4. Duplicate `site/.env.template` and rename it to `site/.env.local`
5. Add proper store values to `site/.env.local`
6. Run `cd site` and `yarn dev` to build and watch for code changes
7. Run `yarn turbo run build` to check the build after your changes

## Work in progress

We're using Github Projects to keep track of issues in progress and todo's. Here is our [Board](https://github.com/vercel/commerce/projects/1)

People actively working on this project: @okbel, @lfades, @dominiksipowicz, @gbibeaul.

## Troubleshoot

<details>
<summary>I already own a BigCommerce store. What should I do?</summary>
<br>
First thing you do is: <b>set your environment variables</b>
<br>
<br>
.env.local

```sh
BIGCOMMERCE_STOREFRONT_API_URL=<>
BIGCOMMERCE_STOREFRONT_API_TOKEN=<>
BIGCOMMERCE_STORE_API_URL=<>
BIGCOMMERCE_STORE_API_TOKEN=<>
BIGCOMMERCE_STORE_API_CLIENT_ID=<>
BIGCOMMERCE_CHANNEL_ID=<>
```

If your project was started with a "Deploy with Vercel" button, you can use Vercel's CLI to retrieve these credentials.

1. Install Vercel CLI: `npm i -g vercel`
2. Link local instance with Vercel and Github accounts (creates .vercel file): `vercel link`
3. Download your environment variables: `vercel env pull .env.local`

Next, you're free to customize the starter. More updates coming soon. Stay tuned..

</details>

<details>
<summary>BigCommerce shows a Coming Soon page and requests a Preview Code</summary>
<br>
After Email confirmation, Checkout should be manually enabled through BigCommerce platform. Look for "Review & test your store" section through BigCommerce's dashboard.
<br>
<br>
BigCommerce team has been notified and they plan to add more details about this subject.
</details>

<details>
<summary>When run locally I get `Error: Cannot find module '...@vercel/commerce/dist/config'`</summary>

```bash
commerce/site
❯ yarn dev
yarn run v1.22.17
$ next dev
ready - started server on 0.0.0.0:3000, url: http://localhost:3000
info  - Loaded env from /commerce/site/.env.local
error - Failed to load next.config.js, see more info here https://nextjs.org/docs/messages/next-config-error
Error: Cannot find module '/Users/dom/work/vercel/commerce/node_modules/@vercel/commerce/dist/config.cjs'
    at createEsmNotFoundErr (node:internal/modules/cjs/loader:960:15)
    at finalizeEsmResolution (node:internal/modules/cjs/loader:953:15)
    at resolveExports (node:internal/modules/cjs/loader:482:14)
    at Function.Module._findPath (node:internal/modules/cjs/loader:522:31)
    at Function.Module._resolveFilename (node:internal/modules/cjs/loader:919:27)
    at Function.mod._resolveFilename (/Users/dom/work/vercel/commerce/node_modules/next/dist/build/webpack/require-hook.js:179:28)
    at Function.Module._load (node:internal/modules/cjs/loader:778:27)
    at Module.require (node:internal/modules/cjs/loader:1005:19)
    at require (node:internal/modules/cjs/helpers:102:18)
    at Object.<anonymous> (/Users/dom/work/vercel/commerce/site/commerce-config.js:9:14) {
  code: 'MODULE_NOT_FOUND',
  path: '/Users/dom/work/vercel/commerce/node_modules/@vercel/commerce/package.json'
}
error Command failed with exit code 1.
info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.
```

The error usually occurs when running yarn dev inside of the `/site/` folder after installing a fresh repository.

In order to fix this, run `yarn dev` in the monorepo root folder first.

> Using `yarn dev` from the root is recommended for developing, which will run watch mode on all packages.

</details>
