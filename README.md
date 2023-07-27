
![Logo](https://ironhack-final-project-theta.vercel.app/assets/logo.3af7e91e.png)


# IronHack - Final Project - Task Organizer

This is the final project for the Ironhack Frontend Bootcamp. 

The goal here is to show everything I learnt during the course, using HTML, CSS, and JavaScript along with the framework "VUE".

In this case, I created a ToDo app with some interesting functions.
For intance: 

- a Login and Singup pages including all the users management behind the scene.
- a Database for tasks and users information.
- a Storage for Avatars. 


## Authors

- [@gabrielberarducci](https://www.github.com/gabrielberarducci)


## 🚀 About Me
I'm a full stack developer...


## Screenshots

<img src="https://github.com/gabrielberarducci/Ironhack_Final_Project/blob/main/assets/img/screenshot%201.png?raw=true" alt="App Login" width="100"/>

![App Home](https://github.com/gabrielberarducci/Ironhack_Final_Project/blob/main/assets/img/screenshot%203.png?raw=true)

![App Add New Task](https://raw.githubusercontent.com/gabrielberarducci/Ironhack_Final_Project/main/assets/img/screenshot%202.png)

![App Profile](https://github.com/gabrielberarducci/Ironhack_Final_Project/blob/main/assets/img/screenshot%204.png?raw=true)

# Proyect Tracking

### Backlog

- ~~Crear funcion de signIn~~
- Buscar como funcionan los metodos de supabase
- Estudiar tienda de tarea
- Estudiar tienda de usuario

### Semana 1

#### Martes - 04/07/23

- Crear funcion de signIn - WIP === Work In Progress
- Crear funcion de signIn - Doing
- Crear funcion de signIn - DONE ✅

#### Jueves - 06/07/23

#### Sabado - 08/07/23

### Semana 2

#### Martes - 11/07/23

#### Jueves - 13/07/23

#### Sabado - 15/07/23

### Semana 3

#### Martes - 18/07/23

#### Jueves - 20/07/23

#### Sabado - 22/07/23


## Environment Variables

To run this project, you will need to add the following environment variables to your .env file

`VITE_SUPABASE_URL`

`VITE_SUPABASE_ANON_KEY`


## Run Locally

Clone the project

```bash
  git clone https://link-to-project
```

Go to the project directory

```bash
  cd my-project
```

Install dependencies

```bash
  npm install
```

Start the server

```bash
  npm run start
```


## Lessons Learned

What did you learn while building this project? What challenges did you face and how did you overcome them?


## Tech Stack

**Client:** VUE, Pinia, Bootstrap, Sweetalert2 

**Server:** Vite, Supabase, Vercel




## Supabase

Imagina que Supabase es como una caja de herramientas mágica para construir sitios web y aplicaciones. Proporciona muchas herramientas listas para usar que facilitan a los desarrolladores crear experiencias en línea poderosas e interactivas.

### Que es Supabase ?

Supabase es una plataforma que te ayuda a crear aplicaciones web y móviles. Es como un conjunto de herramientas y servicios que los desarrolladores utilizan para crear sitios web y aplicaciones más fácilmente. Proporciona una base de datos (donde puedes almacenar información), autenticación (para gestionar usuarios y contraseñas) y almacenamiento de archivos (para guardar y compartir fotos, videos y otros archivos).

### Por que lo usamos ?

Usamos Supabase porque nos facilita la vida como desarrolladores. Nos ahorra tiempo y esfuerzo al proporcionarnos herramientas poderosas y listas para usar. Con Supabase, podemos construir aplicaciones más rápidamente y con menos código. Además, nos permite almacenar información y gestionar usuarios de forma segura y eficiente.

### Ejemplo

Imagina que quieres construir una aplicación de notas en línea. Con Supabase, puedes crear una base de datos para almacenar todas las notas de los usuarios. También puedes agregar autenticación para que los usuarios puedan registrarse y acceder a sus propias notas. Además, puedes usar el almacenamiento de archivos para permitir a los usuarios adjuntar imágenes a sus notas. Supabase se encarga de toda la parte complicada, y tú solo necesitas escribir un poco de código para personalizar la apariencia y el comportamiento de la aplicación.

## Postgres

### Que es postgres?

PostgreSQL, o Postgres en resumen, es un sistema de gestión de bases de datos relacionales. Básicamente, es un software que nos ayuda a almacenar y organizar grandes cantidades de información de manera estructurada. Puedes pensar en ello como una versión avanzada de una hoja de cálculo, pero más potente y capaz de manejar una amplia gama de datos.

### Porque lo usamos ?

Usamos PostgreSQL porque nos permite almacenar y recuperar datos de manera eficiente. Es muy confiable y puede manejar grandes cantidades de información sin problemas. Además, tiene muchas características avanzadas, como el soporte para consultas complejas y la capacidad de mantener la integridad de los datos. Es ampliamente utilizado en aplicaciones empresariales y proyectos grandes donde la precisión y la seguridad de los datos son fundamentales.

## Diff entre postgress y supabase

Supabase:
Supabase es una plataforma de código abierto que combina múltiples herramientas y servicios para simplificar el proceso de construcción de aplicaciones web y móviles. Incluye una base de datos PostgreSQL, un sistema de autenticación y almacenamiento de archivos, entre otras características. Supabase proporciona una configuración lista para usar que facilita a los desarrolladores la creación rápida de aplicaciones. También ofrece capacidades en tiempo real, lo que permite que las aplicaciones actualicen los datos en tiempo real sin requerir actualizaciones manuales.

PostgreSQL:
PostgreSQL, a menudo conocido como Postgres, es un sistema de gestión de bases de datos relacionales (RDBMS) de código abierto, poderoso y altamente confiable. Está diseñado para almacenar y gestionar datos estructurados de manera eficiente. PostgreSQL ofrece un conjunto robusto de características, que incluyen soporte para consultas complejas, integridad de datos, escalabilidad y capacidad de extensión. Se utiliza ampliamente en diversas aplicaciones e industrias, especialmente en proyectos que requieren un alto nivel de integridad de datos, seguridad y escalabilidad.

Diferencias:

Funcionalidad: Supabase se basa en PostgreSQL, lo que significa que utiliza PostgreSQL como su motor de base de datos subyacente. Sin embargo, Supabase agrega herramientas y servicios adicionales, como autenticación y almacenamiento de archivos, para proporcionar una plataforma integrada para la construcción de aplicaciones. PostgreSQL, por otro lado, se centra únicamente en proporcionar un sistema de gestión de bases de datos relacionales potente y flexible.

Facilidad de uso: Supabase ofrece una experiencia más amigable y simplificada para los desarrolladores. Proporciona una configuración simplificada e incluye componentes y bibliotecas preconstruidas que facilitan la construcción de aplicaciones. PostgreSQL, al ser un RDBMS independiente, requiere una configuración y ajuste más manuales.

Capacidades en tiempo real: Una ventaja significativa de Supabase son sus capacidades en tiempo real, que permiten a las aplicaciones escuchar los cambios de datos en tiempo real. Esta función no está disponible solo en PostgreSQL y requiere una implementación y configuración adicionales.

Flexibilidad: Si bien Supabase proporciona una plataforma simplificada e integrada, PostgreSQL ofrece más flexibilidad y control sobre la configuración y la instalación de la base de datos. Con PostgreSQL, los desarrolladores tienen un control total sobre la gestión de la base de datos y pueden personalizarla según sus requisitos específicos.
