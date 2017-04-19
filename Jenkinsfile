node {
    stage ('Checkout') {    
      git url: 'https://github.com/sdara0703/spring-petclinic.git'
      def mvnHome = tool 'Maven350'
      sh "${mvnHome}/bin/mvn clean install -DskipTests=true"
    }
    stage ('Sonar') {
        def mvnHome = tool 'Maven350'
        sh "${mvnHome}/bin/mvn sonar:sonar"
    }
    stage ('Deploy' {
        sh '''
            cd target
            /usr/local/Cellar/tomcat/8.5.14/bin/catalina stop
            rm -rf /usr/local/Cellar/tomcat/8.5.14/libexec/webapps/spring*
            cp -rf spring*.war 
            /usr/local/Cellar/tomcat/8.5.14/bin/catalina start
           ''' 
        
    }
}
