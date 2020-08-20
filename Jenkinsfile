node {
   stage('init') {
      checkout scm
   }
   stage('build') {
      sh '''
         mvn clean
		 mvn package -DskipTest
         cd target
         cp ../src/main/resources/web.config web.config
         mv spring-boot-0.0.1-SNAPSHOT.jar app.jar
		 zip todo.zip app.jar web.config
      '''
   }
   stage('deploy') {
	  echo '000000000000000000'
	  sh 'echo $JAVA_HOME'
   
      azureWebAppPublish azureCredentialsId: env.AZURE_CRED_ID,
      resourceGroup: env.RES_GROUP, appName: env.WEB_APP, filePath: "**/todo.zip"
   }
}