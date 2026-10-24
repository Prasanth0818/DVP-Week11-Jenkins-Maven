# DVP Week 11 — Jenkins + GitHub + Maven CI/CD

A simple Java Maven application for practicing a Jenkins CI/CD pipeline.

## Project structure

```text
DVP-Week11-Jenkins-Maven/
├── pom.xml
├── Jenkinsfile
├── .gitignore
└── src/main/java/com/example/App.java
```

## Requirements

- JDK 21 (or update `maven.compiler.release` in `pom.xml` to your installed JDK)
- Maven 3.8+
- Jenkins with Pipeline and Git plugins; GitHub plugin for webhook triggering

## Run locally

```bash
mvn clean package
java -cp target/jenkins-demo-1.0.0.jar com.example.App
```

Expected application output:

```text
Hello! Jenkins CI/CD Pipeline is working.
```

## Jenkins setup

1. Push this repository to GitHub.
2. In Jenkins, create a **Pipeline** job.
3. Under **Pipeline**, select **Pipeline script from SCM**.
4. SCM: **Git**; enter this repository URL.
5. Branch: `*/main`; Script Path: `Jenkinsfile`.
6. Ensure JDK 21 and Maven are installed and available on the Jenkins agent.
7. Click **Build Now**. The pipeline checks out the source, runs `mvn clean package`, and archives `target/*.jar`.

## GitHub webhook

In GitHub, open **Settings → Webhooks → Add webhook**. Use your publicly reachable Jenkins URL followed by `/github-webhook/`, e.g. `https://YOUR-JENKINS-DOMAIN/github-webhook/`. Set content type to `application/json`. For automatic triggering, enable **GitHub hook trigger for GITScm polling** in the Jenkins job if available.

A webhook secret in GitHub does not by itself guarantee Jenkins validates the signature. Configure a compatible signature-validation mechanism if your environment requires signed webhook verification. Do not commit passwords, access tokens, or webhook secrets.

## Build artifact

After a successful build, Jenkins should show `jenkins-demo-1.0.0.jar` under **Build Artifacts**.
