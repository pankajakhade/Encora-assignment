pipeline{
    agent any
    stages{
        stage("SCM checkout"){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'e319ae26-ad17-4c97-8b99-16535a8304f6', url: 'https://github.com/pankajakhade/Encora-assignment.git']]])
            }
        }
        stage("Build"){
            steps{
                sh "tar --exclude=.git -cvf webserver_${BUILD_NUMBER}.tgz *"
            }
        }
        stage("Deploy to web server"){
            steps{
                sh "scp  -o StrictHostKeyChecking=no -i $HOME/encora.pem webserver_${BUILD_NUMBER}.tgz ubuntu@10.0.2.135:/tmp"
            }
        }
    }
}