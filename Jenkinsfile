pipeline{
    agent any

    tools{
        //this tool :"M2_home" is installed on my local machine not on docker
        maven 'M2_home'
    }
    
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success { 
                    echo "Archiving the artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    
        stage('Deploy to Tomcat server') {
            steps {
            deploy adapters: [tomcat9(credentialsId: 'jenkins_user', path: '', url: 'http://localhost:4004/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}


