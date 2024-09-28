pipeline{
    agent any
        tools {
        maven 'maven' 
    }

    
    stages{
        stage("Test"){
            steps{
                
                sh ' mvn test '
            }
        }
        stage("Build"){
            steps{
                sh "mvn package"
            }
        }
        stage("Deploy into Test"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat10', path: '', url: 'http://13.201.136.247:8080/')], contextPath: '/app', war: '**/*.war'
                
            }
        }
        stage("De3ploy into Prod"){

            input {
                message "Should we continue"
                ok " yes we should"
            }
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat10', path: '', url: 'http://3.108.227.218:8080/')], contextPath: '/app', war: '**/*.war'
                
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
