pipeline {
    agent any
    environment {
        GIT_REPO_URL = 'https://github.com/smidakha/spring-boot-angular-ci-cd.git'
        GIT_BRANCH = 'main'
        JAVA_HOME = tool name: 'JDK17', type: 'jdk' // Make sure JDK11 is configured in Jenkins
        MAVEN_HOME = tool name: 'Maven', type: 'maven' // Make sure Maven is configured in Jenkins
        PATH = "${JAVA_HOME}/bin:${MAVEN_HOME}/bin:${env.PATH}"

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
        
       stage('Setup') {
            steps {
                script {
                    // Install Node.js 20 using nvm
                    
                    sh '''
                        curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
                        export NVM_DIR="${WORKSPACE}/.nvm"
                        [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
                        nvm install 18.19.0
                        nvm use 18.19.0
                        node -v
                    '''
                    
                    
               
                    
                    // Verify the Node.js version
                    sh 'node -v'


                }
            }
        }

        stage('Test Node.js Version') {
            steps {
                script {
                    // Ensure Node.js 20 is installed and being used
                    sh  'node -v'
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
