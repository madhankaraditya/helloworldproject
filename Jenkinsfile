pipeline {
    agent any 

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'mvn clean package' // Adjust this if you're using a different build tool
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'mvn test' // Adjust this if you have a different testing setup
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying..'
                script {
                    def remoteHost = '198.23.164.145' 
                    def remoteDir = '/path/to/deployment/directory' 
                    sshagent(['root-ssh']) { 
                        sh "scp target/your-app.jar root@${remoteHost}:${remoteDir}" 
                        sh "ssh root@${remoteHost} 'java -jar ${remoteDir}/your-app.jar'" 
                    }
                }
            }
        }
    }
}