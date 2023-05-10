pipeline {

  agent any
  environment {
        PLATFORM_CRED = credentials('platform-cred')
        MVN_SET = credentials('maven-settings') 
      }
  stages {
    stage('Build') {
      steps {
            bat 'mvn -B -U -e -V clean -DskipTests package'
      }
    }
	  stage('mvn test settings') {
            steps {
                sh 'mvn -s $MVN_SET help:effective-settings'
            }
        }

    stage('Test') {
      steps {
          echo  'hello world Munit test case'
      }
    }

     stage('Deployment develop')      {
         
         environment {
        CLIENT_ID = credentials('dev-client-d')
        CLIENT_SECRET = credentials('dev-client-secret')
      }
         steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -Pdev -DmuleDeploy -Dusername=%PLATFORM_CRED_USR% -Dpassword=%PLATFORM_CRED_PSW% -Danypoint.platform.client_id=%CLIENT_ID% -Danypoint.platform.client_secret=%CLIENT_SECRET%'
      }
    }
	 stage('Deployment qa')      {
         
         environment {
        CLIENT_ID = credentials('qa-client-id')
        CLIENT_SECRET = credentials('qa-client-secret')
      }
         steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -Pqa -DmuleDeploy -Dusername=%PLATFORM_CRED_USR% -Dpassword=%PLATFORM_CRED_PSW% -Danypoint.platform.client_id=%CLIENT_ID% -Danypoint.platform.client_secret=%CLIENT_SECRET%'
      }
    }
    
  }
}