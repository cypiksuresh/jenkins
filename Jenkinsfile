pipeline {
    agent any
    
    tools {
        maven 'Maven'
    }
    
    stages {
        stage("Test") {
            steps {
                dir('/app') {
                    sh 'mvn test'
                }
                echo "========executing A for Test========"
                // Add your test commands here (e.g., mvn test)
            }
        }
        
        stage("Build") {
            steps {
                sh 'mvn package'
                echo "========executing A for Build========"
                // Add your build commands here (e.g., mvn package)
            }
        }
        
        stage("Deploy on Test") {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcatserverdetails', path: '', url: 'http://34.68.64.209:8080')], contextPath: null, war: '**/*.war'              
                echo "========executing A for Deploy on Test========"
                // Add your deployment commands here (e.g., deploy on container)
            }
        }
        
        stage("Deploy on Prod") {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcatserverdetails', path: '', url: 'http://34.41.46.7:8080')], contextPath: null, war: '**/*.war'              
                echo "Deploying on Production"
                // Add your deployment commands here for production deployment
            }
        }
    }

    post {
        always {
            echo "I will always say hello again"
            // Actions that should always be performed after the pipeline, regardless of success or failure
        }
        failure {
            echo "Pipeline failed!"
            // Actions to be performed only if the pipeline fails
        }
        success {
            echo "Pipeline succeeded!"
            // Actions to be performed only if the pipeline succeeds
        }
    }
}
