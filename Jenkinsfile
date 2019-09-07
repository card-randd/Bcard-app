node('Maven-Label') {
   def mvnHome
   stage('Preparation') {      
      git 'https://github.com/card-randd/Bcard-app.git'
      mvnHome = tool 'Maven'
   }
   stage('Build') {
       withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package sonar:sonar -Dsonar.host.url=http://ec2-52-66-103-154.ap-south-1.compute.amazonaws.com:9000/'
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
