pipeline{
    agent any
    tools {
        maven 'maven' 
    }
    stages{
        stage("Test"){
            steps{
                //mvn test
                sh 'mvn test'
                echo "========executing Test========"
            }
        }
        stage("Build"){
            steps{
                //mvn package
                sh 'mvn package'

                echo "========executing Build========"
            }
        }
        stage("Deploy on Test"){
            steps{
                //deploy on container> Plugin
                deploy adapters: [tomcat9(credentialsId: 'ubuntu', path: '', url: 'http://54.87.36.18:8080')], contextPath: '/app', war: '**/*.war'
                echo "========Deploying to test env========"
            }
        }
        stage("Deploy on Prod"){
            steps{
                //deploy on container> Plugin
                deploy adapters: [tomcat9(credentialsId: 'ubuntu', path: '', url: 'http://54.82.2.98:8080')], contextPath: '/app', war: '**/*.war'
                echo "========Deploying to Prod env========"
            }
        }
    }
    post{
        always{
            echo "========Its completed========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
