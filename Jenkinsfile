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
                sh "tar -cvf webserver_${BUILD_NUMBER}.tgz *"
            }
        }
    }
}