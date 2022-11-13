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
  -Dsonar.host.url=http://192.168.240.131:9000 \
  -Dsonar.login=sqp_86b3ddd6b03ba198747201c5806c306230d3b003"
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
