pipeline{
    agent any
    
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
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://localhost:4004')], contextPath: null, war: '**/*.war'
            }
        }
    }
}


