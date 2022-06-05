pipeline {

  environment {
     def scannerHome = tool 'test'
  }
  
  agent any

  stages {

    stage('Checkout Source') {
      steps {
        checkout scm
      }
    }
    stage("maven build") {
            steps {
                sh 'mvn clean install'
            }
        }
    
    stage("Sonarqube Analyzing") {
            steps {
                sh 'mvn sonar:sonar -Dsonar.projectKey=cankck -Dsonar.host.url=http://192.168.1.214:9000 -Dsonar.login=ac01928679ca493b1b85a181b344d20119684d42'
            }
        }  

        stage("docker build") {
            steps {
                sh 'docker build -t 192.168.1.214:5000/test:v1 .'
            }
        }
        stage("docker upload") {
            steps {
                sh 'docker push 192.168.1.214:5000/test:v1'
            }
        }

        stage('deploy') {
            steps {
                sh 'helm install spring-boot-helloworld -f ./spring-boot-helloworld-chart/values.yaml ./spring-boot-helloworld-chart/'
            }
        }
    }
}
