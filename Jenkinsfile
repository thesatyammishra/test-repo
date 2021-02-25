pipeline {
    agent any
    tools {
        maven 'maven'
        }
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main',
                credentialsId: 'be4829e4-a78c-4a67-a3d0-56e8c1f2c3f4',
                url: 'https://github.com/thesatyammishra/test-repo.git'
                }
        }
        stage ('Clean') {
            steps {
                sh 'mvn clean'
                }
            }
	stage ('Install') {
            steps {
                sh 'mvn install'
                }
            } 
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        
	stage ('Create war file') {
                steps {
                    sh 'jar -cf target/dependency/webapp-runner.jar target/app.war'
                    }
                }
           
         stage ('Deploy War File') {
                 steps {
                   sh "cp target/app.war /home/ec2-user/apache-tomcat-8.5.61/webapps"
                    }
                }
       
    }
}
