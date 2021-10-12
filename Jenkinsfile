pipeline {

  agent any
  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('deploy-anypoint-user')
    MULE_VERSION = '4.3.0'
    BG = "b3f7f859-f414-48c7-9aae-96c5a523fd3e"
    WORKER = "Micro"
  }
  stages {
    stage('Build') {
      steps {
            bat 'mvn clean -DskipTests package -X'
      }
    }

	stage('Deploy Development') {
	  environment {
		ENVIRONMENT = 'Sandbox'
		APP_NAME = 'sandbox-incident-api-sk'
			}
	  steps {
		bat 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version="4.3.0" -Danypoint.username="sudhaoct" -Danypoint.password="Anypoint@2147" -Dcloudhub.app="sandbox-incident-api-sk" -Dcloudhub.environment="Sandbox" -Dcloudhub.bg="b3f7f859-f414-48c7-9aae-96c5a523fd3e" -Dcloudhub.worker="Micro"'
	}
    }
    stage('Deploy Production') {
      environment {
        ENVIRONMENT = 'Production'
        APP_NAME = 'prod-incident-api-sk'
      }
      steps {
            bat 'mvn -U -V -e -B -DskipTests deploy -DmuleDeploy -Dmule.version=$MULE_VERSION -Danypoint.username=$DEPLOY_CREDS_USR -Danypoint.password=$DEPLOY_CREDS_PSW -Dcloudhub.app=$APP_NAME -Dcloudhub.environment=$ENVIRONMENT -Dcloudhub.bg=$BG -Dcloudhub.worker=$WORKER'
      }
    }
  }
}