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

	   stage('Deploy Development') {
      environment {
        ENVIRONMENT = 'Dev'
        APP_NAME = 'mit-jenkins-demo'
      }
      steps {
            bat 'mvn -U -V -e -B -gs %M2SETTINGS% -DskipTests deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%" -Dcloudhub.worker="%WORKER%" -Danypoint.platform.client_id="b6038b7135fe481dba53385f72f00220" -Danypoint.platform.client_secret="674A4ccECb18417e99DC1c0dF346df4f" '
      }
    }
	 stage('Deploy Production') {
      environment {
        ENVIRONMENT = 'PROD'
        APP_NAME = 'mit-jenkins-demo'
      }
      steps {
            bat 'mvn -U -V -e -B -gs %M2SETTINGS% -DskipTests deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%" -Dcloudhub.worker="%WORKER%" -Danypoint.platform.client_id="7893db88a3a14b6e959060013dd7c55e" -Danypoint.platform.client_secret="b1De26Cf58634860a02C0Cfc8ABC0F4e" '
      }
    }

  }

}
