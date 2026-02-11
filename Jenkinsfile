pipeline {
    agent any 
    tools { 
        maven 'maven'
        nodejs 'node'
    }
    stages {
        stage ("Clean up"){
            steps {
                deleteDir()
            }
        }
        stage ("Clone repo"){
            steps {
                sh "git clone https://github.com/MaBouz/tp4jenkins.git"
            }
        }
        stage ("Generate frontend image") {
            steps {
                 dir("tp4jenkins/angular-app"){
                    sh "docker build -t angular-app ."
                }                
            }
        }
        stage ("Generate backend image") {
              steps {
                   dir("tp4jenkins/springboot/app"){
                      sh "mvn clean install"
                      sh "docker build -t springboot-app ."
                  }                
              }
          }
        stage ("Run docker compose") {
            steps {
                 dir("tp4jenkins"){
                    sh " docker-compose up -d"
                }                
            }
        }
    }
}
