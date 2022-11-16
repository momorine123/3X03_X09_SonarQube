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
sh "${scannerHome}/bin/sonar-scanner \
   -Dsonar.projectKey=OWASP \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://192.168.1.133:9000 \
  -Dsonar.login=sqp_ef741769360ab19980bd7123bc9b47fd88cf0922"
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