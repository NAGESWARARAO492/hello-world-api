pipeline {

  agent any
  environment {
        PLATFORM_CRED = credentials('platform-cred')
        
      }
  stages {
    stage('Build') {
      steps {
            bat 'mvn -B -U -e -V clean -DskipTests package'
      }
    }
	 
    stage('Test') {
      steps {
          echo  'hello world Munit test case'
      }
    }

     stage('Deployment dev')      {
         
         environment {
        CLIENT_ID = credentials('dev-client-d')
        CLIENT_SECRET = credentials('dev-client-secret')
        CAPPCLIENT_ID = credentials('connectedAppClient_id')
        CAPPCLIENT_SECRET = credentials('connectedAppClient_secret')
      }
         steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -Pdev -DmuleDeploy -DconnectedAppClientId=%CAPPCLIENT_ID% -DconnectedAppClientSecret=%CAPPCLIENT_SECRET% -Danypoint.platform.client_id=%CLIENT_ID% -Danypoint.platform.client_secret=%CLIENT_SECRET%'
      }
    }
	 stage('Deployment qa')      {
         
         environment {
        CLIENT_ID = credentials('qa-client-id')
        CLIENT_SECRET = credentials('qa-client-secret')
      }
         steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -Pqa -DmuleDeploy -DconnectedAppClientId=%CAppCLIENT_ID% -DconnectedAppClientSecret=%CAppCLIENT_SECRET% -Danypoint.platform.client_id=%CLIENT_ID% -Danypoint.platform.client_secret=%CLIENT_SECRET%'
      }
    }
    
  }
}
