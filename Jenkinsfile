node('Maven-Label') {
   def mvnHome
   stage('Preparation') {      
      git 'https://github.com/card-randd/Bcard-app.git'
      mvnHome = tool 'Maven'
   }
   stage('Build') {
       withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
}
