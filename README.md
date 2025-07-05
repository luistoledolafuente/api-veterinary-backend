# API Veterinary - Backend

Sistema de gestión veterinaria desarrollado en **Laravel 11** (PHP 8.2), diseñado para administrar citas médicas, historiales clínicos, pagos, usuarios, notificaciones y reportes en una clínica veterinaria.

---

## Tabla de Contenidos
- [Descripción General](#descripción-general)
- [Tecnologías y Librerías](#tecnologías-y-librerías)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Instalación y Configuración](#instalación-y-configuración)
- [Variables de Entorno](#variables-de-entorno)
- [Migraciones y Seeders](#migraciones-y-seeders)
- [Ejecución y Scripts](#ejecución-y-scripts)
- [Pruebas](#pruebas)
- [Buenas Prácticas y Decisiones Técnicas](#buenas-prácticas-y-decisiones-técnicas)
- [Notas de Seguridad](#notas-de-seguridad)
- [Licencia](#licencia)

---

## Descripción General

Este backend expone una API RESTful para la gestión integral de una veterinaria, permitiendo:

- Registro y gestión de usuarios, roles y permisos.
- Administración de mascotas, veterinarios y personal.
- Gestión de citas médicas, vacunaciones y cirugías.
- Control de pagos y estados de deuda.
- Notificaciones automáticas por correo y SMS (AWS SNS).
- Exportación de reportes en Excel.

El objetivo es centralizar y automatizar los procesos administrativos y médicos de una clínica veterinaria, facilitando la trazabilidad y la comunicación con los clientes.

---

## Tecnologías y Librerías

### Framework y Lenguaje
- **Laravel 11**: Framework PHP robusto, elegido por su arquitectura MVC, facilidad para crear APIs, seguridad y comunidad activa.
- **PHP 8.2**: Versión moderna, con mejoras de rendimiento y tipado estricto.

### Librerías Principales
- **maatwebsite/excel (^3.1)**: Permite exportar reportes en Excel, útil para informes administrativos y de gestión médica.
- **spatie/laravel-permission (^6.9)**: Gestión avanzada de roles y permisos, facilitando la administración de accesos según perfiles.
- **php-open-source-saver/jwt-auth (^2.3)**: Autenticación basada en JWT, ideal para APIs seguras y escalables.
- **aws/aws-sdk-php (^3.328)**: Integración con AWS SNS para envío de SMS y notificaciones, mejorando la comunicación con clientes.
- **laravel/sanctum (^4.0)**: Autenticación ligera para SPAs y aplicaciones móviles.
- **axios**: Cliente HTTP usado en el frontend para consumir la API.

### Herramientas de Desarrollo
- **Vite**: Bundler moderno para recursos frontend, rápido y eficiente.
- **PHPUnit**: Framework de testing para PHP, asegurando la calidad del código.

---

## Estructura del Proyecto

```
.
├── app/                # Lógica de negocio, controladores, modelos, policies, providers
├── bootstrap/          # Bootstrap de Laravel
├── config/             # Configuración de servicios, base de datos, mail, etc.
├── database/           # Migraciones, seeders y factories
├── public/             # Punto de entrada público (index.php)
├── resources/          # Vistas y assets frontend
├── routes/             # Definición de rutas (api.php, web.php)
├── storage/            # Archivos generados y logs
├── tests/              # Pruebas unitarias y funcionales
├── .env                # Variables de entorno
├── composer.json       # Dependencias PHP
├── package.json        # Dependencias JS
└── README.md           # Documentación principal
```

---

## Instalación y Configuración

1. **Clonar el repositorio**
   ```sh
   git clone <url-del-repo>
   cd api_veterinary
   ```
2. **Instalar dependencias PHP**
   ```sh
   composer install
   ```
3. **Instalar dependencias JS**
   ```sh
   npm install
   ```
4. **Configurar variables de entorno**
   - Copia `.env.example` a `.env` y ajusta los valores según tu entorno.
   - Configura la conexión a base de datos PostgreSQL, credenciales de correo y AWS SNS.
5. **Generar clave de aplicación**
   ```sh
   php artisan key:generate
   ```

---

## Variables de Entorno

Algunas variables clave en `.env`:

- **Base de datos**
  ```
  DB_CONNECTION=pgsql
  DB_HOST=127.0.0.1
  DB_PORT=5432
  DB_DATABASE=veterinary
  DB_USERNAME=postgres
  DB_PASSWORD=******
  ```
- **Correo**
  ```
  MAIL_MAILER=smtp
  MAIL_HOST=smtp.gmail.com
  MAIL_PORT=465
  MAIL_USERNAME=xxxx@gmail.com
  MAIL_PASSWORD=********
  MAIL_ENCRYPTION=ssl
  MAIL_FROM_ADDRESS="admin@example.com"
  ```
- **AWS SNS (SMS)**
  ```
  AWS_ACCESS_KEY_ID=...
  AWS_SECRET_ACCESS_KEY=...
  AWS_DEFAULT_REGION=sa-east-1
  AWS_PHONE="tunumero"
  ```
- **JWT**
  ```
  JWT_SECRET=...
  JWT_ALGO=HS256
  ```

---

## Migraciones y Seeders

1. **Ejecutar migraciones**
   ```sh
   php artisan migrate
   ```
2. **Cargar datos de prueba (seeders)**
   ```sh
   php artisan db:seed
   ```
   Puedes ejecutar seeders específicos, por ejemplo:
   ```sh
   php artisan db:seed --class=PermissionsDemoSeeder
   ```

---

## Ejecución y Scripts

- **Servidor de desarrollo**
  ```sh
  php artisan serve
  ```
- **Compilar assets frontend**
  ```sh
  npm run dev
  ```
- **Compilar para producción**
  ```sh
  npm run build
  ```
- **Tareas programadas (notificaciones)**
  - Se recomienda configurar un cron para ejecutar los comandos Artisan:
    ```sh
    php artisan schedule:run
    ```

---

## Pruebas

- **Ejecutar pruebas unitarias y funcionales**
  ```sh
  ./vendor/bin/phpunit
  ```
- Las pruebas se encuentran en el directorio [`tests/`](tests/).

---

## Buenas Prácticas y Decisiones Técnicas

- **MVC y separación de responsabilidades:** Se sigue el patrón Modelo-Vista-Controlador para mantener el código organizado y escalable.
- **Uso de migraciones y seeders:** Permite versionar la base de datos y poblarla fácilmente en diferentes entornos.
- **Autenticación JWT:** Proporciona seguridad y escalabilidad para APIs modernas.
- **Roles y permisos:** Implementados con Spatie para un control granular de accesos.
- **Notificaciones y comunicación:** Integración con AWS SNS y correo electrónico para mantener informados a los usuarios.
- **Testing:** Se promueve el uso de pruebas unitarias y funcionales para asegurar la calidad y robustez del sistema.
- **Variables de entorno:** Toda la configuración sensible y dependiente del entorno se gestiona desde `.env`.
- **Documentación:** Este README sirve como guía principal para desarrolladores y usuarios del sistema.

---

## Notas de Seguridad

- **Nunca subas tu archivo `.env` ni credenciales sensibles a repositorios públicos.**
- Cambia las claves de acceso y tokens antes de desplegar en producción.
- Usa HTTPS en producción para proteger la transmisión de datos.

---

## Licencia

Este proyecto utiliza la licencia [MIT](https://opensource.org/licenses/MIT).
