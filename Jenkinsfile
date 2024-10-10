pipeline {
    agent any 

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'mvn clean package' // Example for Maven; adjust as needed
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'mvn test' // Example for Maven; adjust as needed
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying..'
                script {
                    def remoteHost = '198.23.164.145' // Your server IP
                    def remoteDir = '/path/to/deployment/directory' // Change this to your desired path
                    sshagent(['root-ssh']) { // Use the credential ID you will create
                        sh "scp target/your-app.jar root@${remoteHost}:${remoteDir}" // Adjust the jar path
                        sh "ssh root@${remoteHost} 'java -jar ${remoteDir}/your-app.jar'" // Adjust the jar execution command
                    }
                }
            }
        }
    }
}