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
                sshPublisher(publishers: [sshPublisherDesc(configName: 'web', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''sudo mkdir -p /var/www/webserver_${BUILD_NUMBER}
cd /tmp
sudo tar -xvf webserver_${BUILD_NUMBER}.tgz -C /var/www/webserver_${BUILD_NUMBER}
sudo rm -rf /var/www/html
sudo ln -s /var/www/webserver_${BUILD_NUMBER} /var/www/html
sudo service nginx restart''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'webserver_${BUILD_NUMBER}.tgz')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}