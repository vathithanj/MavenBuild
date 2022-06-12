node{
   stage('SCM Checkout'){
       git credentialsId: 'git_creds', url: 'https://github.com/vathithanj/MavenBuild.git'
   }
   stage('Mvn Package'){
     sh "mvn clean package"
   }
   stage('Build Docker Image'){
     sh 'docker build -t vathithan/my-cicd-app:1.0.0 .'
   }
   stage('Push Docker Image'){
     withCredentials([string(credentialsId: 'dockerHub-Pwd', variable: 'dockerHubPwd')]) {
        sh "docker login -u vathithan -p ${dockerHubPwd}"
     }
     sh 'docker push vathithan/my-cicd-app:1.0.0'
   }
   stage('Run Container on worker Server'){
     def dockerRun = 'docker run -p 8080:8080 -d --name my-cicd-app vathithan/my-cicd-app:1.0.0'
     sshagent(['worker-server']) {
       sh "ssh -o StrictHostKeyChecking=no ubuntu@54.211.235.31 ${dockerRun}"       
     }
   }
}
