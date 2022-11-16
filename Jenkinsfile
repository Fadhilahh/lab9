pipeline {
    agent any
    stages {
        stage ('Checkout') {
            steps {
                git branch:'master', url: 'https://github.com/OWASP/Vulnerable-Web-Application.git'
        }
    }
    stage('Code Quality Check via SonarQube') {
        steps {
            script {
                def scannerHome = tool 'SonarQube';
                withSonarQubeEnv('SonarQube') {
                sh "${scannerHome}/bin/sonar-scanner.bat -D"sonar.projectKey=OWASP" -D"sonar.sources=." -D"sonar.host.url=http://localhost:9000" -D"sonar.login=sqp_d113ffccb03e324450f29701f46efcaefa3429ee""
         }
      }
    }
   }
}
post {
    always {
        recordIssues enabledForFailure: true, tool: sonarQube()
    }
  }
}
