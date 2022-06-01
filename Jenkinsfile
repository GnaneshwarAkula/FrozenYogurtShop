pipeline {
    agent any
    stages {
        stage('Build') {
            steps {                
                git 'https://github.com/GnaneshwarAkula/FrozenYogurtShop.git'
                sh "docker build -t gnaakula/newweb001:${env.BUILD_TAG} ."
            }
        }
        stage('Push') {
            steps {
                sh "docker push gnaakula/newweb001:${env.BUILD_TAG}"
            }
        }
        stage('Deploy') {
            steps {
                sh "sed -i 's/username/${env.BUILD_TAG}/g' k8s-deploy.yaml"
                sh "kubectl apply -f k8s-deploy.yaml"
                sh "kubectl get svc | grep ${env.BUILD_TAG}"
            }
        }
      
    }
}
