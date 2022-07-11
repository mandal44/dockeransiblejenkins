pipeline{
    agent any
    tools {
      maven 'maven_3'
    }
    stages{
        stage('SCM'){
            steps{
                git credentialsId: 'github', 
                    url: 'https://github.com/mandal44/dockeransiblejenkins.git'
            }
        }
        
        stage('Maven Build'){
            steps{
                sh "mvn clean package"
            }
        }
        
        stage('Docker Build'){
            steps{
                sh "docker build . -t mandal44/newrepo:1.0.0.1"
            }
        }
        
        stage('DockerHub Push'){
            steps{
                
                sh "docker login -u mandal44 -p Docker@45"
                sh "docker push mandal44/newrepo:1.0.0.1 "
            }
        }
        
        stage('Docker Deploy'){
            steps{
              ansiblePlaybook credentialsId: 'dev-server', disableHostKeyChecking: true, installation: 'ansible', inventory: 'dev.inv', playbook: 'deploy-docker.yml'
        
                
            }
        }
        
        
    }
}

