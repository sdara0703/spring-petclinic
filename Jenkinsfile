node {
    
    properties([[$class: 'BuildDiscarderProperty', strategy: [$class: 'LogRotator', artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '5', numToKeepStr: '5']]]);
    
    def mvnHome = tool 'Maven350'
    
    stage ('Checkout from GIT') {    
      git url: 'https://github.com/sdara0703/spring-petclinic.git'
      //def mvnHome = tool 'Maven350'
      sh "${mvnHome}/bin/mvn clean install -DskipTests=true"
    }
    stage ('Sonar Scan') {
        //def mvnHome = tool 'Maven350'
        sh "${mvnHome}/bin/mvn sonar:sonar"
    }
    stage ('Nexus Upload') {
        //def mvnHome = tool 'Maven350'
        sh "${mvnHome}/bin/mvn deploy -DskipTests=true"
    }
    stage ('Deploy to Tomcat') {
        sh '''
            cd target
            sudo /usr/local/Cellar/tomcat/8.5.14/bin/catalina stop
            sudo rm -rf /usr/local/Cellar/tomcat/8.5.14/libexec/webapps/spring*
            sudo cp -rf spring*.war /usr/local/Cellar/tomcat/8.5.14/libexec/webapps/
            sudo /usr/local/Cellar/tomcat/8.5.14/bin/catalina start
           ''' 
    }
}
