# docker
1. Создаем Docker-образ 
docker build -t practice:1.0.0 .

2. Запускаем контейнер 
docker run -d --name practice -p 8080:8000 practice:1.0.0

3. Переходим по адресу http://127.0.0.1:8080/hello.html 
Видим "Hello world"

4. Выкладываем образ на Docker Hub
docker login
docker tag practice:1.0.0 alexey14011/practice:1.0.0
docker push alexey14011/practice:1.0.0

5. Создаем deployment.yaml файл

6. Применяем манифест 
kubectl apply -f deployment.yaml

7. Обеспечиваем доступ к web-приложению
kubectl port-forward --address 0.0.0.0 deployment/web 8080:8000

8. Результат выполнения кода kubectl describe deployment web”




PS C:\Users\Alexey\Desktop\study\ИТМО\devops\docker> kubectl describe deployment web  
Name:                    web  
Namespace:               default  
CreationTimestamp:       Mon, 22 May 2023 01:52:21 +0300  
Labels:                  <none>  
Annotations:             deployment.kubernetes.io/revision: 1  
Selector:                app=web  
Replicas:                2 desired | 2 updated | 2 total | 2 available | 0 unavailable  
StrategyType:            RollingUpdate  
MinReadySeconds:         0  
RollingUpdateStrategy:   25% max unavailable, 25% max surge  
Pod Template:  
  Labels:   app=web  
  Containers:  
   web:  
    Image:          alexey14011/practice:1.0.0  
    Port:           8000/TCP  
    Host Port:      0/TCP  
    Liveness:       http-get http://:8000/hello.html delay=15s timeout=1s period=20s #success=1 #failure=3  
    Readiness:      http-get http://:8000/hello.html delay=5s timeout=1s period=10s #success=1 #failure=3  
    Environment:    <none>  
    Mounts:         <none>  
  Volumes:          <none>  
Conditions:  
  Type             Status  Reason  
  ----             ------  ------  
  Available        True    MinimumReplicasAvailable  
  Progressing      True    NewReplicaSetAvailable  
OldReplicaSets:    <none>  
NewReplicaSet:     web-84d58f787d (2/2 replicas created)  
Events:  
  Type     Reason              Age    From                    Message  
  ----     ------              ----   ----                    -------  
  Normal   ScalingReplicaSet   6m1s   deployment-controller   Scaled up replica set web-84d58f787d to 2  
