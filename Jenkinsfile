def testmethod(String name = 'human'){
   echo Test,"$(name)"
}
node ("maven-label"){
   
   stage("ref lib"){
      
      testmethod 'test'
   }
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/cicd-tools-0/ycard.git'
                 
      mvnHome = tool 'maven-3.6.0'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }
}
