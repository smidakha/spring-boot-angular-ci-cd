pipeline {
    agent any
    environment {
        GIT_REPO_URL = 'https://github.com/smidakha/spring-boot-angular-ci-cd.git'
        GIT_BRANCH = 'main'
        JAVA_HOME = tool name: 'JDK17', type: 'jdk' // Make sure JDK11 is configured in Jenkins
        MAVEN_HOME = tool name: 'Maven', type: 'maven' // Make sure Maven is configured in Jenkins
        PATH = "${JAVA_HOME}/bin:${MAVEN_HOME}/bin:${env.PATH}"
        NODE_HOME = tool name: 'NodeJS20.15.1', type: 'node'
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
                       dir('/var/lib/jenkins/workspace/pipeline-back/spring-boot-angular-16-crud-example/spring-boot-server') {
                        sh 'mvn spring-boot:run'
                        echo "test"

              			 }

   				   }
				}
				}
	   stage('Build Frontend') {
            steps {
                script {
                    dir('/var/lib/jenkins/workspace/pipeline-back/spring-boot-angular-16-crud-example/angular-16-client') {
                     sh 'node -v'
                    }
                }
            }
        }
			}
    	}


       

    	

    }   

}
