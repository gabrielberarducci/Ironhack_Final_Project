
<img src="https://ironhack-final-project-theta.vercel.app/assets/logo.3af7e91e.png" alt="Logo" width="500"/>

## Web App

- [Visit the App](https://ironhack-final-project-theta.vercel.app/)

# IronHack - Final Project - Task Organizer

This is the final project for the Ironhack Frontend Bootcamp. 

The goal here is to show everything I learnt during the course, using HTML, CSS, and JavaScript along with the framework "VUE".

In this case, I created a ToDo app with some interesting functions.
For intance: 

- a Login and Singup pages including all the users management behind the scene.
- a Database for tasks and users information.
- a Storage for Avatars. 

## Presentation

- [Presentation](https://www.canva.com/design/DAFp5ujyyU0/J72Nwfnc83V1Ko5IBsizGg/view?utm_content=DAFp5ujyyU0&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink)

## Authors

- [@gabrielberarducci](https://www.github.com/gabrielberarducci)

## Screenshots

<h4>Login</h4><img src="https://github.com/gabrielberarducci/Ironhack_Final_Project/blob/main/assets/img/screenshot%201.png?raw=true" alt="App Login" width="300"/>
<h4>Home</h4><img src="https://github.com/gabrielberarducci/Ironhack_Final_Project/blob/main/assets/img/screenshot%203.png?raw=true" alt="App Home" width="300"/>
<h4>Add New Task</h4><img src="https://github.com/gabrielberarducci/Ironhack_Final_Project/blob/main/assets/img/screenshot%202.png?raw=true" alt="App Add new task" width="300"/>
<h4>Profile</h4><img src="https://github.com/gabrielberarducci/Ironhack_Final_Project/blob/main/assets/img/screenshot%204.png?raw=true" alt="App Profile" width="300"/>

# Proyect Tracking

### Semana 1

#### Martes - 04/07/23

- Create signIn function- DONE✅
- Create signUp function - DONE✅
- Create Logout function - DONE✅

#### Jueves - 06/07/23

- Create all the actions for the task store - DONE✅
- Create the TaskItem and NewTask components - DONE✅
  
#### Sabado - 08/07/23

- Configure Supabase with a new "profile" table - DONE✅
- Create the Profile component - DONE✅
- Create the Account view - DONE✅
  

### Semana 2

#### Martes - 11/07/23

- Check "edit profile" functionality - DONE✅
- Create Storage in Supabase - DONE✅
- implement the Avatar utilization in the profile component - DONE✅
- Implement a button to hide the forms for "NewTask", "EditProfile" and "ChangeAvatar" - DONE✅

#### Jueves - 13/07/23

- Create the NavBar Component - DONE✅
- Implement the Profile picture with the dropdown menu in the navbar - DONE✅
- Create the brand and the logo - DONE✅

#### Sabado - 15/07/23

- Add bootstrap to the project - DONE✅
- Investigate functionalities of bootstrap - DONE✅
- Create the CSS for SignIn / SingUp views - DONE✅
- Create the CSS for Home - DONE✅
- Create the CSS for Account - DONE✅

### Semana 3

#### Martes - 25/07/23

- Include Sweetalert2 for Messages and Popups - DONE✅
- Create the Documentation / Readme - DONE✅

#### Jueves - 27/07/23

- Create the Presentation - DONE✅
- Complete the Ironhack Portal tasks - DONE✅

#### Sabado - 29/07/23

- Presentation perform

## Environment Variables

To run this project, you will need to add the following environment variables to your .env file

`VITE_SUPABASE_URL`

`VITE_SUPABASE_ANON_KEY`


## Run Locally

Clone the project

```bash
  git clone https://github.com/gabrielberarducci/Ironhack_Final_Project.git
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
  npm run dev
```


## Tech Stack

**Client:** VUE, Pinia, Bootstrap, Sweetalert2 

**Server:** Vite, Supabase, Vercel

Supabase

Imagine Supabase as a magical toolbox for building websites and applications. It provides many ready-to-use tools that make it easy for developers to create powerful and interactive online experiences.
What is Supabase?

Supabase is a platform that helps you create web and mobile applications. It's like a set of tools and services that developers use to build websites and applications more easily. It provides a database (where you can store information), authentication (for managing users and passwords), and file storage (for saving and sharing photos, videos, and other files).
Why do we use it?

We use Supabase because it simplifies our lives as developers. It saves us time and effort by providing powerful, ready-to-use tools. With Supabase, we can build applications more quickly and with less code. Additionally, it allows us to store information and manage users securely and efficiently.
Example

Imagine you want to build an online note-taking application. With Supabase, you can create a database to store all the users' notes. You can also add authentication so that users can sign up and access their own notes. Furthermore, you can use file storage to allow users to attach images to their notes. Supabase takes care of all the complex parts, and you only need to write a little bit of code to customize the appearance and behavior of the application.
PostgreSQL
What is PostgreSQL?

PostgreSQL, or simply Postgres, is a relational database management system (RDBMS). Essentially, it is software that helps us store and organize large amounts of structured information. You can think of it as an advanced version of a spreadsheet but more powerful and capable of handling a wide range of data.
Why do we use it?

We use PostgreSQL because it allows us to store and retrieve data efficiently. It is highly reliable and can handle large amounts of information seamlessly. Additionally, it has many advanced features, such as support for complex queries and the ability to maintain data integrity. It is widely used in enterprise applications and large projects where data accuracy and security are essential.
Diff between PostgreSQL and Supabase

Supabase:
Supabase is an open-source platform that combines multiple tools and services to simplify the process of building web and mobile applications. It includes a PostgreSQL database, authentication system, file storage, among other features. Supabase provides a ready-to-use setup that makes it easy for developers to quickly create applications. It also offers real-time capabilities, allowing applications to update data in real-time without requiring manual refreshes.

PostgreSQL:
PostgreSQL, often known as Postgres, is a powerful and highly reliable open-source relational database management system (RDBMS). It is designed to store and manage structured data efficiently. PostgreSQL offers a robust set of features, including support for complex queries, data integrity, scalability, and extensibility. It is widely used in various applications and industries, especially in projects that require a high level of data integrity, security, and scalability.

Differences:

Functionality: Supabase is built on PostgreSQL, meaning it uses PostgreSQL as its underlying database engine. However, Supabase adds additional tools and services like authentication and file storage to provide an integrated platform for application building. PostgreSQL, on the other hand, focuses solely on providing a powerful and flexible relational database management system.

Ease of use: Supabase offers a more user-friendly and simplified experience for developers. It provides a streamlined setup and includes pre-built components and libraries that make application building easier. PostgreSQL, being a standalone RDBMS, requires more manual setup and tweaking.

Real-time capabilities: A significant advantage of Supabase is its real-time capabilities, allowing applications to listen for data changes in real-time. This feature is not available in PostgreSQL alone and requires additional implementation and configuration.

Flexibility: While Supabase provides a simplified and integrated platform, PostgreSQL offers more flexibility and control over database configuration and setup. With PostgreSQL, developers have full control over managing the database and can customize it to their specific requirements.
