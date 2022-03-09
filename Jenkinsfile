node {

stage("Git Clone"){

        git credentialsId: 'GIT_HUB_CREDENTIALS', url: 'https://github.com/deepsardana/springboot-with-docker.git'
    }
stage('Gradle Build') {

       sh './gradlew build'

    }
stage("Docker build"){
        sh 'docker version'
        sh 'docker build -t demo .'
        sh 'docker image list'
        sh 'docker tag demo deep77/spring:latest'
    }
stage("Docker Login"){
        withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
            sh 'docker login -u deep77 -p $PASSWORD'
        }
    }
stage("Push Image to Docker Hub"){
        sh 'docker push  deep77/spring:latest'
    }
stage("copy k8 file into k8 server" ){
        'scp -i deep.pem -r springboot-with-docker/k8s-spring-boot-deployment.yml ubuntu@34.205.140.91:/home/ubuntu'
    }
stage("SSH Into k8s Server") {
        'ssh -i deep.pem ubuntu@34.205.140.91'
    }
stage("deploy Pod into K8 Server") {
        'kubectl apply -f k8s-spring-boot-deployment.yml'
    }    
}   
