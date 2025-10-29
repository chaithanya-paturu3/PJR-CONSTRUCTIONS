# PJR-CONSTRUCTIONS

Absolutely! Here’s an **expanded, step-by-step description** including how to create Docker tokens and add secrets in GitHub Actions. You can use this directly in your README.

---

# PJR-Constructions Docker CI/CD Process

This project demonstrates building, containerizing, and deploying a simple web landing page using **Docker** and **GitHub Actions** for CI/CD automation.

---

## **1. Project Structure**

* `.github/workflows/` → Contains GitHub Actions workflow (`dockerci.yml`) to automate Docker image build and push.
* `pjr-constructions/` → Application folder with landing page code (`index.html`, `styles.css`) and `Dockerfile`.
* `README.md` → Project documentation.

---

## **2. Setting Up the Project**

1. Create your landing page inside the `pjr-constructions` folder.
2. Add a **Dockerfile** in the same folder:

   * Choose a base image (e.g., Nginx).
   * Copy landing page files into the container.
   * Expose port 80 for HTTP access.

---

## **3. Creating a Docker Hub Personal Access Token (PAT)**

1. Log in to [Docker Hub](https://hub.docker.com/).
2. Go to **Account Settings → Security → New Access Token**.
3. Give it a descriptive name (e.g., `GitHub Actions`) and generate the token.
4. Copy the token — this will be used as your password in GitHub Actions.

---

## **4. Adding Secrets in GitHub Actions**

1. Open your repository on GitHub.
2. Go to **Settings → Secrets and variables → Actions → New repository secret**.
3. Add two secrets:

   * `DOCKER_USERNAME` → Your Docker Hub username (e.g., `chaithu33`).
   * `DOCKER_PASSWORD` → The Docker PAT you just created.
4. These secrets allow GitHub Actions to securely log in to Docker Hub without exposing credentials in the workflow.

---

## **5. Configuring GitHub Actions**

1. Add a workflow in `.github/workflows/dockerci.yml`.
2. Configure it to trigger on pushes to the `main` branch.
3. Workflow steps:

   * **Checkout** the repository so files are accessible.
   * **Set up Docker Buildx** to enable multi-platform builds.
   * **Login to Docker Hub** using the secrets for username and password.
   * **Build and push** the Docker image:

     * Use `pjr-constructions` as the build context.
     * Tag the image with your Docker Hub username.
     * Push the image to Docker Hub automatically.

---

## **6. Docker Build Context**

* The **build context** is the folder Docker can access during the build.
* All paths in the Dockerfile are **relative to the build context**.
* Correct usage: `COPY . /usr/share/nginx/html`
* Avoid absolute paths (like `/pjr-constructions`) in the Dockerfile.

---

## **7. Docker Image on Docker Hub**

* After a successful workflow, the image is available on Docker Hub under your account.
* Example: `chaithu33/pjr-constructions:latest`
* It can be pulled and run on any machine with Docker.

---

## **8. Running the Container Locally**

1. Pull the image from Docker Hub:

```bash
docker pull chaithu33/pjr-constructions:latest
```

2. Run the container and map port 80 to your local port:

```bash
docker run -d -p 8080:80 chaithu33/pjr-constructions:latest
```

3. Open your browser and visit:

```
http://localhost:8080
```

You will see your PJR-Constructions landing page.

---

## **9. Key Learnings**

* How to Dockerize a web application.
* How to set up CI/CD using GitHub Actions.
* How to securely manage credentials using GitHub secrets and Docker PATs.
* Understanding Docker build context and best practices for Dockerfiles.
* Automating Docker image build and deployment.

---

