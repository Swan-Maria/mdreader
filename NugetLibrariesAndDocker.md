## Libraries

In programming, a **library** is a reusable collection of code that provides pre-built functionality. It can contain functions, classes, and other resources that are compiled and ready to use. Think of a library as a toolbox full of specialized tools. Instead of creating a new hammer for every nail, you just grab the existing one from the toolbox. This modular approach saves time and effort, as you can leverage code that has already been tested and debugged.

## NuGet Packages

A **NuGet package** is essentially a zipped file with a `.nupkg` extension that contains a library, along with metadata like its version number and dependencies on other packages. It's the standard way to package and share code in the .NET world. While a library is the code itself, a NuGet package is the standardized, distributable container for that code. It simplifies the process of getting a library and all its necessary files into your project.

## NuGet Manager

The **NuGet Package Manager** is the tool that facilitates the use of NuGet packages. It's built into development environments like Visual Studio and can also be used via a command-line interface. Its primary function is to manage the lifecycle of packages in your project. It can:
- **Search** for packages from public or private repositories.
- **Install** packages and their dependencies.
- **Update** packages when new versions are available.
- **Remove** packages you no longer need.

This tool automates the process of adding and managing dependencies, ensuring that your project has the correct files and references it needs to run properly.


## Docker

Docker is an open-source platform that simplifies the process of building, shipping, and running applications by using **containers**. A container packages an application and all its dependencies (like libraries, tools, and code) into a single, isolated, and portable unit. This ensures that the application runs consistently, regardless of the environment it's deployed in, solving the common "it works on my machine" problem.

### How it Works

Docker uses a **client-server architecture**.
- The **Docker client** is the command-line interface (CLI) that users interact with.
- The **Docker daemon (dockerd)** runs in the background and manages Docker objects like images, containers, and networks.

The core components of Docker are **Images** and **Containers**.
- A **Docker Image** is a read-only blueprint that contains the application and all the instructions needed to create a running container. Think of it as a template. Images are created from a text file called a **Dockerfile**, which specifies the steps to build the image, such as what operating system to use and which packages to install.
- A **Docker Container** is a runnable instance of an image. It's a lightweight, isolated environment where the application actually runs. You can start, stop, move, or delete containers using simple commands. A single image can be used to create multiple containers, each running independently.

### Key Features and Benefits

- **Portability:** Docker containers can run on any system with Docker installed, from a developer's laptop to a production server in the cloud, ensuring a consistent environment.
- **Efficiency:** Unlike traditional virtual machines (VMs) that require their own full operating system, containers share the host machine's OS kernel. This makes them much more lightweight, start up faster, and use fewer resources.
- **Isolation:** Containers run in their own isolated environments, preventing conflicts between applications and dependencies. This also enhances security by separating applications from the host system and each other.
- **Faster Development and Deployment:** Docker streamlines the development workflow. By using containers, developers can work in environments that are identical to production, which significantly reduces compatibility issues and speeds up the delivery process. Docker integrates seamlessly with CI/CD (Continuous Integration/Continuous Deployment) pipelines.

### Docker Compose

Docker Compose is a tool that simplifies the management of multi-container applications by using a single YAML file to define how the different parts of an application should run together. It's a layer of abstraction on top of Docker itself.


### Commands

#### Run a Single Container

To run a single container, you use the **`docker run`** command, specifying the image you want to use and any configuration options. A common example is running a web server like Nginx.

```bash
docker run --name my-nginx-container -p 8080:80 -d nginx
```

**Explanation:**
- **`docker run`**: The command to create and run a new container.
- **`--name my-nginx-container`**: Assigns a custom name to the container for easier management.
- **`-p 8080:80`**: Maps port `8080` on your host machine to port `80` inside the container. This allows you to access the Nginx web server from your browser at `http://localhost:8080`.
- **`-d`**: Runs the container in **detached mode** (in the background), so it doesn't tie up your terminal.
- **`nginx`**: The name of the Docker image to use. If the image isn't available locally, Docker will automatically pull it from Docker Hub.

#### Run a Compose File

For applications with multiple services (e.g., a web app and a database), you use **Docker Compose**. First, you create a configuration file named `docker-compose.yml` that defines all your services. Then, you use a single command to start them all.
```bash
docker compose up
```

**Explanation:**
- **`docker compose up`**: This command reads the `docker-compose.yml` file, builds the images (if needed), creates the containers, sets up a shared network for them to communicate, and starts all the defined services. You can add the `-d` flag to run them in detached mode.


## Links

Docker: https://www.docker.com/get-started/
Docker Hub: https://hub.docker.com/
