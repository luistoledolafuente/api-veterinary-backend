# 🐾 API Veterinary - Backend

¡Bienvenido al backend de gestión veterinaria!  
Este proyecto, construido con **Laravel 11** (PHP 8.2), está diseñado para digitalizar y automatizar la administración de clínicas veterinarias: desde la gestión de pacientes peludos hasta la comunicación con sus humanos.  
¡Optimiza tu clínica, ahorra tiempo y mejora la experiencia de tus clientes! 🚀

---

## 📚 Tabla de Contenidos

- [📝 Descripción General](#-descripción-general)
- [🛠️ Tecnologías y Librerías](#️-tecnologías-y-librerías)
- [📁 Estructura del Proyecto](#-estructura-del-proyecto)
- [⚙️ Instalación y Configuración](#️-instalación-y-configuración)
- [🔑 Variables de Entorno](#-variables-de-entorno)
- [🗄️ Migraciones y Seeders](#️-migraciones-y-seeders)
- [🏃 Ejecución y Scripts](#-ejecución-y-scripts)
- [🧪 Pruebas](#-pruebas)
- [💡 Buenas Prácticas y Decisiones Técnicas](#-buenas-prácticas-y-decisiones-técnicas)
- [🔒 Notas de Seguridad](#-notas-de-seguridad)
- [📄 Licencia](#-licencia)

---

## 📝 Descripción General

Esta API RESTful permite gestionar todos los procesos clave de una clínica veterinaria:

- 🐶 **Pacientes:** Registro y administración de mascotas.
- 👩‍⚕️ **Personal:** Gestión de veterinarios y usuarios.
- 📅 **Citas:** Programación y control de consultas, vacunaciones y cirugías.
- 💳 **Pagos:** Control de pagos y estados de deuda.
- 📧 **Notificaciones:** Comunicación automática por correo y SMS (AWS SNS).
- 📊 **Reportes:** Exportación de datos en Excel para análisis y control.

**Objetivo:**  
Centralizar y automatizar los procesos administrativos y médicos, facilitando la trazabilidad, la seguridad y la comunicación con los clientes.

---

## 🛠️ Tecnologías y Librerías

### Framework y Lenguaje

- **Laravel 11**  
  Elegido por su arquitectura MVC, robustez, seguridad y comunidad activa.
- **PHP 8.2**  
  Versión moderna, con tipado estricto y mejoras de rendimiento.

### Librerías Principales

- **maatwebsite/excel (^3.1)**  
  Exporta reportes en Excel, ideal para informes administrativos y médicos.
- **spatie/laravel-permission (^6.9)**  
  Control granular de roles y permisos.
- **php-open-source-saver/jwt-auth (^2.3)**  
  Autenticación JWT, estándar para APIs seguras y escalables.
- **aws/aws-sdk-php (^3.328)**  
  Integración con AWS SNS para SMS y notificaciones.
- **laravel/sanctum (^4.0)**  
  Autenticación ligera para SPAs y apps móviles.
- **axios**  
  Cliente HTTP para consumir la API desde el frontend.

### Herramientas de Desarrollo

- **Vite**  
  Bundler moderno, rápido y eficiente para recursos frontend.
- **PHPUnit**  
  Testing robusto para asegurar la calidad del código.

---

## 📁 Estructura del Proyecto

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

## ⚙️ Instalación y Configuración

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

## 🔑 Variables de Entorno

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

## 🗄️ Migraciones y Seeders

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

## 🏃 Ejecución y Scripts

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

## 🧪 Pruebas

- **Ejecutar pruebas unitarias y funcionales**
  ```sh
  ./vendor/bin/phpunit
  ```
- Las pruebas se encuentran en el directorio [`tests/`](tests/).

---

## 💡 Buenas Prácticas y Decisiones Técnicas

- **MVC y separación de responsabilidades:** Se sigue el patrón Modelo-Vista-Controlador para mantener el código organizado y escalable.
- **Uso de migraciones y seeders:** Permite versionar la base de datos y poblarla fácilmente en diferentes entornos.
- **Autenticación JWT:** Proporciona seguridad y escalabilidad para APIs modernas.
- **Roles y permisos:** Implementados con Spatie para un control granular de accesos.
- **Notificaciones y comunicación:** Integración con AWS SNS y correo electrónico para mantener informados a los usuarios.
- **Testing:** Se promueve el uso de pruebas unitarias y funcionales para asegurar la calidad y robustez del sistema.
- **Variables de entorno:** Toda la configuración sensible y dependiente del entorno se gestiona desde `.env`.
- **Documentación:** Este README sirve como guía principal para desarrolladores y usuarios del sistema.

---

## 🔒 Notas de Seguridad

- **Nunca subas tu archivo `.env` ni credenciales sensibles a repositorios públicos.**
- Cambia las claves de acceso y tokens antes de desplegar en producción.
- Usa HTTPS en producción para proteger la transmisión de datos.

---

## 📄 Licencia

Este proyecto utiliza la licencia [MIT](https://opensource.org/licenses/MIT).
