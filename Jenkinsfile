pipeline {
    agent any
    
    tools{
        maven "Maven-3.9.9"
    }    

    stages {
        stage('Git Clone') {
            steps {
               git branch: 'main', url: 'https://github.com/pnegi5106/contact_backend_app.git'
            }
        }
        stage('Maven Build'){
            steps{
             sh 'mvn clean package'
            }
        }
        stage('Docker Image'){
            steps{
             sh 'docker build -t pradeep332/contact_backend_app .'
            }
        }
        stage('Docker Image push'){
            steps{
            withCredentials([string(credentialsId: 'docker_pwd', variable: 'docker_pwd')]) {
                   sh 'docker login -u pradeep332 -p ${docker_pwd}'
                   sh 'docker push pradeep332/contact_backend_app'
            }
            }
        }
        stage('k8s deployment'){
            steps{
             sh 'kubectl apply -f Deployment.yml'
            }
        }        
    }
}
