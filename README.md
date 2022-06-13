This is a sample web application.

Use Maven Build first to create war file in Target folder.

mvn clean package

Artifact will be created in target folder.

Then build the docker image.

Deploy the image on the docker container (woreker-server)

Then access the application using http://<<IP Address of woreker-server>>:8080/my-cicd-app
