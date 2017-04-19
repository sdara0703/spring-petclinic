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
}
