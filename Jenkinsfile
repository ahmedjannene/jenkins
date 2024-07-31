pipeline {
    agent any

    tools {
        // Ensure the Maven tool is installed and configured correctly in Jenkins
        maven 'M2_home'
    }

    stages {
        stage('Build') {
            steps {
                // Run Maven to build the project and create the WAR file
                sh 'mvn clean package'
                
                // List the contents of the target directory to verify WAR file creation
                sh 'ls -l target'
            }
            post {
                success {
                    echo "Archiving the artifacts"
                    // Archive the WAR file as a build artifact
                    archiveArtifacts artifacts: '**/target/*.war', allowEmptyArchive: false
                }
            }
        }
    
        stage('Deploy to Tomcat server') {
            steps {
                // Deploy the WAR file to Tomcat using the specified credentials and URL
                deploy adapters: [
                    tomcat9(
                        credentialsId: 'jenkins_user',  // Replace with your actual credentials ID
                        url: 'http://tomcat:4004/manager/text'  // Ensure 'tomcat' is the correct service name
                    )
                ],
                contextPath: '',  // Deploy to the root context
                war: '**/target/*.war'  // Ensure the path to the WAR file is correct
            }
        }
    }
}
