pipeline {

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
                sh 'helm install --name spring-boot-helloworld -f ./spring-boot-helloworld-chart/values.yaml ./spring-boot-helloworld-chart/'
            }
        }
    }
}
