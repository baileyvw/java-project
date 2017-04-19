pipeline {
  agent none

  stages {
    stage('Unit Tests') {
      agent {
        label 'apache'
      }
      steps {
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
       }
      }
      stage('build') {
         agent {
           label 'apache'
         }
        steps {
          sh 'ant -f build.xml -v'
        }
     }
     stage('deploy') {
        agent {
          label 'apache'
        }
        steps {
         sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all/"
        }
       } 
     stage("Running centos") {
       agent {
         label 'centos'
       }  
      }

   post {
     always {
        archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
     }
   }
 }
