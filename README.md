
## 🔎 Descripción de la Arquitectura

<details>
  <summary>🧅 Onion Architecture</summary>
  
La `Arquitectura Onion` propone organizar el código de tal manera que el **dominio** de la aplicación se encuentre en el **núcleo** del sistema, protegiéndolo de cambios en los **frameworks** y **tecnologías externas**. El objetivo es mantener la **lógica de negocio** aislada y evitar acoplamientos directos con la infraestructura. Esta arquitectura se basa en **capas concéntricas** que interactúan entre sí y define cuatro capas principales:

1. **`Domain` (Núcleo del Dominio):** Contiene las entidades y reglas de negocio puras.
2. **`Application` (Aplicación):** Contiene los **casos de uso** y la lógica de la aplicación que utiliza el dominio.
3. **`Infrastructure` (Infraestructura):** Provee implementaciones concretas para las **interfaces** definidas por el dominio, como acceso a **bases de datos**, **servicios externos**, etc.
4. **`Presentation` (Interfaz / Presentación):** Se encarga de interactuar con el **usuario final** o con otros sistemas, manejando la **entrada y salida** de la aplicación (por ejemplo, APIs REST).

</details>

<details>
  <summary>🧩 Hexagonal Architecture</summary>

La `Arquitectura Hexagonal`, también conocida como **Arquitectura de Puertos y Adaptadores**, permite que la aplicación sea **independiente** de las **entradas y salidas** (tecnologías y frameworks) gracias a la **separación clara** entre la **lógica de negocio** y la **infraestructura**. Define dos conceptos clave:

- **Puertos:** `Interfaces` que representan la forma en que la aplicación interactúa con el mundo exterior.
- **Adaptadores:** Implementaciones concretas que permiten que la aplicación interactúe con tecnologías específicas (por ejemplo, `bases de datos`, `APIs`).

Esta combinación permite crear aplicaciones **flexibles** y fácilmente adaptables a **cambios tecnológicos**.

</details>

## 🏗️ Estructura y Convenciones

<details>
  <summary>📂 Estructura del proyecto </summary>

```bash
/src
  /- application
    /- use_cases         # Lógica de los casos de uso
    /- services          # Servicios que apoyan a los casos de uso
    /- dto               # Data Transfer Objects
    /- exceptions        # Clases de excepciones personalizadas
  /- domain
    /- entities          # Entidades del dominio (lógica de negocio)
    /- repositories      # Interfaces para la capa de infraestructura
  /- infrastructure
    /- persistence       # Implementación de los repositorios (bases de datos)
    /- orm               # Configuraciones de ORM si aplican
    /- external_services # Llamadas a servicios externos (APIs, etc.)
  /- interfaces
    /- rest
      /- controller      # Controladores REST que manejan las solicitudes HTTP
      /- routes          # Definición de rutas de la API
      /- middleware      # Middlewares como validaciones, autenticación, etc.
    /- Server.ts         # Inicialización del servidor y configuración de Express
  /- console
  / etc.
  ```
</details>

<details>
    <summary> 📂 Responsabilidades de las Carpetas</summary>


### `/application`
- **Responsabilidad:** Contiene la lógica específica de la aplicación, incluyendo casos de uso y servicios que interactúan con el dominio.
- **Subcarpetas:**
  - **`/use_cases`:** Implementación de los casos de uso de la aplicación.
  - **`/services`:** Servicios que apoyan la lógica de los casos de uso.
  - **`/dto`:** Data Transfer Objects utilizados para la comunicación entre capas.
  - **`/exceptions`:** Clases de excepciones personalizadas utilizadas en la aplicación.

### `/domain`
- **Responsabilidad:** Define las entidades y las reglas de negocio puras.
- **Subcarpetas:**
  - **`/entities`:** Clases que representan los objetos de dominio con sus atributos y comportamientos.
  - **`/repositories`:** Interfaces para las operaciones de persistencia definidas por el dominio.

### `/infrastructure`
- **Responsabilidad:** Implementaciones concretas para acceder a recursos externos, como bases de datos o servicios de terceros.
- **Subcarpetas:**
  - **`/persistence`:** Implementaciones de los repositorios para la persistencia de datos.
  - **`/orm`:** Configuraciones específicas del Object-Relational Mapping (ORM).
  - **`/external_services`:** Implementaciones para interactuar con servicios externos (APIs, microservicios, etc.).

### `/interfaces`
- **Responsabilidad:** Maneja la interacción con el usuario o con otros sistemas, definiendo las rutas y controladores.
- **Subcarpetas:**
  - **`/rest`:** Contiene controladores y rutas para las APIs REST.
    - **`/controller`:** Controladores que gestionan las solicitudes y respuestas HTTP.
    - **`/routes`:** Definición de las rutas de la API.
    - **`/middleware`:** Middlewares utilizados para la validación y autenticación.
    - **`Server.ts`:** Inicialización del servidor y configuración de Express.
  - **`/console`:** Comandos o scripts para ser ejecutados en la consola.

### `/etc`
- **Responsabilidad:** Contiene otros archivos de configuración o scripts que no encajan en las otras categorías.

</details>


<details>
  <summary>📜 Convenciones de Entidades</summary>
    
 - Para mantener la **consistencia** y **claridad** en el desarrollo del proyecto, seguiremos las siguientes  reglas para `entidades`, `repositorios`, `casos de uso`, etc.

### 🏷️ Nombres de Entidades:
- Las entidades del dominio deben tener nombres en **singular** y en `**inglés**`.
- **Ejemplo:** `Product`, `User`, `Order`.

### 📦 Nombres de Repositorios:
- Los repositorios deben seguir el patrón `I<Entity>Repository` para las **interfaces** y `<Entity>Repository` para las **implementaciones**.
- **Ejemplo:** `IProductRepository`, `ProductRepository`.

### 🔄 Nombres de Casos de Uso:
- Los casos de uso deben describir claramente la **acción** que realizan y estar en **inglés**.
- **Ejemplo:** `CreateProduct`, `GetUserById`.

### 📨 DTOs (Data Transfer Objects):
- Los DTOs deben tener nombres que reflejen claramente su **propósito** y estar en **inglés**.
- **Ejemplo:** `ProductDTO`, `UserDTO`.

### 🔧 Servicios:
- Los servicios deben tener nombres que reflejen claramente su **propósito** y estar en **inglés**.
- **Ejemplo:** `EmailService`, `PaymentService`.

### ⚠️ Excepciones:
- Las excepciones personalizadas deben tener nombres que reflejen claramente el **error** y estar en **inglés**.
- **Ejemplo:** `ProductNotFoundException`, `InvalidUserException`.

Estas convenciones nos ayudarán a mantener un código **limpio** y **fácil de entender**, facilitando la **colaboración** y el **mantenimiento** del proyecto.
</details>

<details> <summary>📄 Convenciones de Nombres de Archivos</summary>

### Nombres de Repositorios:
- **Formato:** `<nombre_entidad>.repository.ts`
- **Ejemplo:** `user.repository.ts`, `product.repository.ts`

### Nombres de Controladores:
- **Formato:** `<nombre_entidad>.controller.ts`
- **Ejemplo:** `user.controller.ts`, `product.controller.ts`

### Nombres de Servicios:
- **Formato:** `<nombre_servicio>.service.ts`
- **Ejemplo:** `email.service.ts`, `payment.service.ts`

### Nombres de DTOs (Data Transfer Objects):
- **Formato:** `<nombre_entidad>.dto.ts`
- **Ejemplo:** `user.dto.ts`, `product.dto.ts`

### Nombres de Casos de Uso:
- **Formato:** `<nombre_caso_uso>.useCase.ts`
- **Ejemplo:** `createUser.useCase.ts`, `getProductById.useCase.ts`

### Nombres de Excepciones:
- **Formato:** `<nombre_error>.exception.ts`
- **Ejemplo:** `productNotFound.exception.ts`, `invalidUser.exception.ts`

### Nombres de Interfaces:
- **Formato:** `I<nombre_entidad>.ts`
- **Ejemplo:** `IUser.ts`, `IProduct.ts`

### Nombres de Middleware:
- **Formato:** `<nombre_middleware>.middleware
</details>

