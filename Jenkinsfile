pipeline {
  agent any
  stages {
    stage("test") {
      steps {
        bat 'gradlew test'
        junit 'build/test-results/test/TEST-Matrix.xml'
        cucumber buildStatus: 'UNSTABLE', reportTitle: 'My report',  fileIncludePattern: 'target/report.json',  trendsLimit: 10
      }  
    }
    
    stage('build') {
      steps {
        bat(script: 'gradlew build', label: 'gradlew build')
        bat 'gradlew javadoc'
        archiveArtifacts 'build/libs/*.jar'
        junit(testResults: 'build/reports/tests/test', allowEmptyResults: true)
      }
    }
    
    
    
    
    
}

}
