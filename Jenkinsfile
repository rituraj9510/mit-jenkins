pipeline {
	//Test
  agent any
  environment {
    //adding a comment for the commit test
    DEPLOY_CREDS = credentials('deploy-anypoint-user')
    MULE_VERSION = '4.4.0'
    BG = "Apisero"
    WORKER = "Micro"
    M2SETTINGS = "C:\\Users\\riturajrgupta\\.m2\\settings.xml"
  }
  stages {
    stage('Build') {
      steps {
            bat 'mvn -B -U -e -V clean -gs %M2SETTINGS% -DskipTests package'
      }
    }

	 stage('Deploy Production') {
      environment {
        ENVIRONMENT = 'Production'
        APP_NAME = 'mit-jenkins-demo-1'
      }
      steps {
            bat 'mvn -U -V -e -B -gs %M2SETTINGS% -DskipTests deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%" -Dcloudhub.worker="%WORKER%" -Danypoint.platform.client_id="59ba5066d99344289ddf42592a14d9fd" -Danypoint.platform.client_secret="321fFaCE921d448aB0C8E75aB6e4d9a3" '
      }
    }

  }

}
