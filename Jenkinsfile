pipeline {
  agent any
  stages {
    stage('compile') {
      steps {
        sh './gradlew compileJava'
      }
    }
    stage('code coverage') {
      steps {
        sh './gradlew jacocoTestReport'
        publishHTML (target: [
          reportDir: 'build/reports/jacoco/test/html',
          reportFiles: 'index.html',
          reportName: "JaCoCo Report"
        ])
        sh './gradlew jacocoTestCoverageVerification'
      }
    }
    stage('static code analysis') {
      steps {
        sh './gradlew checkstyleMain'
        publishHTML (target: [
          reportDir: 'build/reports/checkstyle/',
          reportFiles: 'main.html',
          reportName: "Checkstyle Report"
        ])
      }
    }
    stage('unit test') {
      steps {
        sh './gradlew test'
      }
    }
  }
}
