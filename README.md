# Books
Developed a basic spring boot application and pushed the images to the docker repo.

Steps to follow to spawn the containers locally and perform CRUD operations on the book table of the Books database.

## Steps
1) Clone the git repository using ```git clone https://github.com/VSNSAINIVAS/Books.git```.
2) Make sure minikube and kubectl are installed by using commands ```minikube version``` & ```kubectl version```.
3) Start the minikube by using ```minikube start --driver=<driver_name>``` (Driver name should be replaced by the name of the driver examples: docker, hyperv etc.)
4) Replace **MYSQL_ROOT_PASSWORD**, **MYSQL_PASSWORD** values in mysql-secret with base64 encoded value of the original value.
5) Replace **SPRING_DATASOURCE_PASSWORD** valuues in springboot-secret with base64 encoded value of the original value.
6) Apply the mysql deployment using ```kubectl create -f mysql.yaml```.
7) After creating the deployment login to mysql pod using ```kubectl exec -it <pod_id> -- bash```.
8) Login to mysql using ```mysql -u<User_name> -p<Password>```.
   Create a table using commands
   ```
   CREATE TABLE IF NOT EXISTS book ( 
    book_id INT AUTO_INCREMENT PRIMARY KEY, 
    book_title VARCHAR(255), 
    book_author VARCHAR(255), 
    bookisbn VARCHAR(255), 
    book_abstract TEXT 
    );
   ```
9) Apply the spring-boot deployment using ```kubectl create -f springboot.yaml```.
10) Get the url of the spring-boot service using ```minikube service <service_name> --url```.
