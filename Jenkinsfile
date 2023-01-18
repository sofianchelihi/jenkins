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
    
    stage('Deploy') {
      steps {
        bat 'gradlew publish'
        
      }
    }
    
    
     stage('Notification') {
      steps {
       notifyEvents message: 'Build success', token: 'v9rftHtfpE--B5rwyQF1TBpJlRhoicwn'
      }
    }
}
  
  post {
    success {
          mail(subject: 'Build Success', body: 'New Build is deployed !', from: 'ja_manaa@esi.dz', to: 'ja_manaa@esi.dz')
     }
    failure {
          mail(subject: 'Build Failure', body: "the new build isn't deployed succesfully !", from: 'ja_manaa@esi.dz', to: 'ja_manaa@esi.dz')
     }    
   }
}
