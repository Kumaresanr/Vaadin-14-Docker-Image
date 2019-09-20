# Vaadin-14-Docker-Image - Parent Image for Vaadin 14

Besides Java, [Vaadin 14](https://vaadin.com/docs/v14/index.html) also requires Node.js. This image could be used as a parent image for custom Docker images. But it could also used by CI/CD pipelines like the one of [GitLab](https://docs.gitlab.com/ee/ci/).

For installing Node.js, the [frontend-maven-plugin](https://github.com/eirslett/frontend-maven-plugin/) could be used as well. However, its installed Node.js version is not meant for production.

## .gitlab-ci.yml Example

The example is an excerpt from the .gitlab-ci.yml and just shows the build stage. The build app uses Vaadin 14 and Spring Boot. As a build automation tool, Maven is used.

```yml
image: seifertfelix/vaadin14:14-jdk-alpine

stages:
  - build
  - deploy

before_script:
  - chmod +x mvnw

build:
  stage: build
  script:
    - ./mvnw clean package -Pproduction -e
  artifacts:
    paths:
      - target/*.jar
```
