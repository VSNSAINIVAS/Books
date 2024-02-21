# Books
Developed a basic spring boot application and pushed the images to the docker repo.

Steps to follow to create the containers locally and perform CRUD operations on the book table of the Books database.

## Note:
### Make sure you modify the version of the image which is being pulled based on the architecture of the system. If you are using ARM architecture use tag (v1) and if you are using AMD architecture use tag (v2).

## Steps (Without Helm)
1) Clone the git repository using ```git clone https://github.com/VSNSAINIVAS/Books.git```.
2) Make sure minikube and kubectl are installed by using commands ```minikube version``` & ```kubectl version```.
3) Start the minikube by using ```minikube start --driver=<driver_name>``` (Driver name should be replaced by the name of the driver examples: docker, hyperv etc.)
4) Replace **MYSQL_ROOT_PASSWORD**, **MYSQL_PASSWORD** values in mysql-secret with base64 encoded value of the original value.
5) Replace **SPRING_DATASOURCE_PASSWORD** valuues in springboot-secret with base64 encoded value of the original value.
6) Apply configmaps for mysql and secrets for it using the commands ```kubectl create -f mysql-config-map.yaml``` && ```kubectl create -f mysql-secret.yaml```
7) Apply configmaps for springboot and secrets for it using the command ```kubectl create -f springboot-config-map.yaml``` && ```kubectl create -f springboot-secret.yaml```
8) Apply the mysql deployment using ```kubectl create -f mysql.yaml```.
9) Apply the spring-boot deployment using ```kubectl create -f springboot.yaml```.
10) Get the url of the spring-boot service using ```minikube service <service_name> --url```.
11) Copy the url and this is needed for testing.
12) Use this documentation to perform CRUD operations locally https://documenter.getpostman.com/view/32443384/2sA2r82jLB#313efa48-0a5e-4a58-be14-984d4c464e0a. (Make sure to replace the first url part from http://127.0.0.1/<port number> with the url of service which you obtained in above step.)

## Steps (With Helm)
1) Make sure you add the helm repo with the command ```helm repo add books-springboot https://vsnsainivas.github.io/springboot-books-helm```.
2) Then install the helm chart using ```helm install books-springboot/springboot```.
