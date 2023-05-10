pipeline {

  agent any
  environment {
		 CAPPCRED = credentials('ConnectedAppCred')
            }
  stages {
    stage('Build') {
    
      steps {
            bat 'mvn -B -U -e -V clean -DskipTests package -Duser=%CAPPCRED_USR% -Dpswd=%CAPPCRED_PSW%'
      }
    }

    stage('Test') {
      steps {
          echo  'hello world Munit test case'
      }
    }

     stage('Deployment dev')      {
         
         environment {
		CAPPCLIENT_ID = credentials('connectedAppClient_id')
        CAPPCLIENT_SECRET = credentials('connectedAppClient_secret')
        CLIENT_ID = credentials('dev-client-d')
        CLIENT_SECRET = credentials('dev-client-secret')
		
      }
         steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -Pdev -DmuleDeploy -DconnectedAppClientId=%CAPPCLIENT_ID% -DconnectedAppClientSecret=%CAPPCLIENT_SECRET% -Danypoint.platform.client_id=%CLIENT_ID% -Danypoint.platform.client_secret=%CLIENT_SECRET%'
      }
    }
	 stage('Deployment qa')      {
         
         environment {
		 CAPPCLIENT_ID = credentials('connectedAppClient_id')
        CAPPCLIENT_SECRET = credentials('connectedAppClient_secret')
        CLIENT_ID = credentials('qa-client-id')
        CLIENT_SECRET = credentials('qa-client-secret')
      }
         steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -Pqa -DmuleDeploy -DconnectedAppClientId=%CAPPCLIENT_ID% -DconnectedAppClientSecret=%CAPPCLIENT_SECRET% -Danypoint.platform.client_id=%CLIENT_ID% -Danypoint.platform.client_secret=%CLIENT_SECRET%'
      }
    }
    
  }
}