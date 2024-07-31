pipeline {
    agent any
    environment {
        GIT_REPO_URL = 'https://github.com/smidakha/spring-boot-angular-ci-cd.git'
        GIT_BRANCH = 'main'
        SPRINGBOOT_IMAGE = 'spring-boot-app'
        ANGULAR_IMAGE = 'angular-app'

    }

    stages {
      
        stage('Checkout') {
            steps {
                script {
                    // Perform Git checkout
                    checkout([$class: 'GitSCM', 
                        branches: [[name: env.GIT_BRANCH]],
                        userRemoteConfigs: [[url: env.GIT_REPO_URL]]
                    ])
                }
            }
        }
        
        stage('parallel stage') {
          parallel {
           stage('Build Backend') {
             steps {
                script {
                    cd /projects/spring-boot-angular-16-crud-example/spring-boot-server
                    sh 'docker build -t ${SPRINGBOOT_IMAGE} .'
                }
            }
				}
	   stage('Build Frontend') {
	    steps {
                script {
                    cd /projects/spring-boot-angular-16-crud-example/angular-16-client
                    sh 'docker build -t ${ANGULAR_IMAGE} .'
                }
            }

        }
       
		}
    	}
    	
    	stage('Deploy') {
            steps {
                script {
                    // Example of running containers
                    sh 'docker run -d --name springboot-app -p 8081:8081 ${SPRINGBOOT_IMAGE}'
                    sh 'docker run -d --name angular-app -p 8082:8082 ${ANGULAR_IMAGE}'
                }
            }
        }
    }
 
      post {
        always {
            script {
                // Clean up any running containers
                sh 'docker rm -f spring-boot-app || true'
                sh 'docker rm -f angular-app || true'
            }
        }
    }
}
