
## Описание

В данном проекте используется Minikube для развертывания Kubernetes кластера, в котором мы активируем Ingress и создаем сервис `app`, доступный через Ingress.

## Шаги выполнения

### 1. Запуск Minikube и активация Ingress

1. Установите Minikube, если он еще не установлен.
2. Запустите Minikube:
   ```sh
   minikube start
   ```
3. Активируйте Ingress в Minikube:
   ```sh
   minikube addons enable ingress
   ```

### 2. Применение Kubernetes манифестов

Создайте и примените следующие манифесты:

#### Деплоймент для сервиса `app`

Файл: `app-deployment.yaml`
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app
  labels:
    app: app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: app
  template:
    metadata:
      labels:
        app: app
    spec:
      containers:
      - name: app
        image: your-app-image:latest
        ports:
        - containerPort: 8080
```

#### Сервис для `app`

Файл: `app-service.yaml`
```yaml
apiVersion: v1
kind: Service
metadata:
  name: app
spec:
  selector:
    app: app
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080
```

#### Ingress для `app`

Файл: `app-ingress.yaml`
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /app/*
        pathType: Prefix
        backend:
          service:
            name: app
            port:
              number: 8080
```

Примените манифесты:
```sh
kubectl apply -f app-deployment.yaml
kubectl apply -f app-service.yaml
kubectl apply -f app-ingress.yaml
```

### 3. Проверка работы Ingress

1. Узнайте IP-адрес Minikube:
   ```sh
   minikube ip
   ```
2. Отправьте запрос на сервис:
   ```sh
   curl http://<MINIKUBE_IP>/app/
   ```
   Замените `<MINIKUBE_IP>` на IP-адрес, который вы получили.

### 4. Отслеживание логов Pod'ов

Просмотрите логи одного из Pod'ов сервиса `app`:
```sh
kubectl logs <app-pod-name>
```
Замените `<app-pod-name>` на имя одного из Pod'ов.

## Репозиторий

Репозиторий содержит следующие файлы:
- `app-deployment.yaml`: Деплоймент для сервиса `app`.
- `app-service.yaml`: Сервис для `app`.
- `app-ingress.yaml`: Ingress для `app`.

## Лицензия

Этот проект лицензируется на условиях MIT License. Подробнее см. в файле [LICENSE](LICENSE).

## Контакты
Конечно! Вот пример README файла для вашего репозитория на GitHub:

```markdown
# Kubernetes Ingress Demo

Этот репозиторий содержит манифесты Kubernetes и инструкции по настройке Ingress для публикации сервиса `app` наружу кластера Minikube.

## Описание

В данном проекте используется Minikube для развертывания Kubernetes кластера, в котором мы активируем Ingress и создаем сервис `app`, доступный через Ingress.

## Шаги выполнения

### 1. Запуск Minikube и активация Ingress

1. Установите Minikube, если он еще не установлен.
2. Запустите Minikube:
   ```sh
   minikube start
   ```
3. Активируйте Ingress в Minikube:
   ```sh
   minikube addons enable ingress
   ```

### 2. Применение Kubernetes манифестов

Создайте и примените следующие манифесты:

#### Деплоймент для сервиса `app`

Файл: `app-deployment.yaml`
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app
  labels:
    app: app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: app
  template:
    metadata:
      labels:
        app: app
    spec:
      containers:
      - name: app
        image: your-app-image:latest
        ports:
        - containerPort: 8080
```

#### Сервис для `app`

Файл: `app-service.yaml`
```yaml
apiVersion: v1
kind: Service
metadata:
  name: app
spec:
  selector:
    app: app
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080
```

#### Ingress для `app`

Файл: `app-ingress.yaml`
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /app/*
        pathType: Prefix
        backend:
          service:
            name: app
            port:
              number: 8080
```

Примените манифесты:
```sh
kubectl apply -f app-deployment.yaml
kubectl apply -f app-service.yaml
kubectl apply -f app-ingress.yaml
```

### 3. Проверка работы Ingress

1. Узнайте IP-адрес Minikube:
   ```sh
   minikube ip
   ```
2. Отправьте запрос на сервис:
   ```sh
   curl http://<MINIKUBE_IP>/app/
   ```
   Замените `<MINIKUBE_IP>` на IP-адрес, который вы получили.

### 4. Отслеживание логов Pod'ов

Просмотрите логи одного из Pod'ов сервиса `app`:
```sh
kubectl logs <app-pod-name>
```
Замените `<app-pod-name>` на имя одного из Pod'ов.

## Репозиторий

Репозиторий содержит следующие файлы:
- `app-deployment.yaml`: Деплоймент для сервиса `app`.
- `app-service.yaml`: Сервис для `app`.
- `app-ingress.yaml`: Ingress для `app`.
