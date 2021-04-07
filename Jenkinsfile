stage('SonarScan')
{
steps
{
def sonarScanner(projectKey) {
    def scannerHome = tool 'SonarQubeScanner'
    withSonarQubeEnv("sonarqube") {
        if(fileExists("sonar-project.properties")) {
            sh "${scannerHome}/bin/sonar-scanner"
        }
        else {
            sh "${scannerHome}/bin/sonar-scanner -     Dsonar.projectKey=${projectKey} -Dsonar.java.binaries=build/classes -Dsonar.java.libraries=**/*.jar -Dsonar.projectVersion=${BUILD_NUMBER}"
        }
    }
    timeout(time: 10, unit: 'MINUTES') {
        waitForQualityGate abortPipeline: true
    }
}
}
}
