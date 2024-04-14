# Домашнее задание к занятию "`Домашнее задание к занятию «GitLab»`" - `Бакулев Евгений`

### Задание 1
### Что нужно сделать:

1. Разверните GitLab локально, используя Vagrantfile и инструкцию, описанные в этом репозитории.
2. Создайте новый проект и пустой репозиторий в нём.
3. Зарегистрируйте gitlab-runner для этого проекта и запустите его в режиме Docker. Раннер можно регистрировать и запускать на той же виртуальной машине, на которой запущен GitLab.

В качестве ответа в репозиторий шаблона с решением добавьте скриншоты с настройками раннера в проекте.

### Решение 1

![Скрин](https://github.com/garrkiss/8-03-hw/blob/main/img/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2014.04.24_21.10.12.png)

### Задание 2
### Что нужно сделать:

1. Запушьте репозиторий на GitLab, изменив origin. Это изучалось на занятии по Git.
2. Создайте .gitlab-ci.yml, описав в нём все необходимые, на ваш взгляд, этапы.
   
В качестве ответа в шаблон с решением добавьте:
- файл gitlab-ci.yml для своего проекта или вставьте код в соответствующее поле в шаблоне;
- скриншоты с успешно собранными сборками.

### Решение 2


```
stages:
  - test
  - static-analysis
  - build

test:
  stage: test
  image: golang:1.17
  script: 
   - go test .

static-analysis:
 stage: test
 image:
  name: sonarsource/sonar-scanner-cli
  entrypoint: [""]
 variables:
 script:
  - sonar-scanner -Dsonar.projectKey=my_project -Dsonar.sources=. -Dsonar.host.url=http://158.160.118.158:9000 -Dsonar.login=sqp_e8fe2deba4be4ae3d3fff9fcf0a5fcc61b0a9467

build:
  stage: build
  image: docker:latest
  script:
   - docker build .
```

![Скрин](https://github.com/garrkiss/8-03-hw/blob/main/img/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2014.04.24_22.36.31.png)
