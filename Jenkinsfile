pipeline {
  agent any
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          post {
            success {
              archiveArtifacts(artifacts: 'java-app/target/*.jar', fingerprint: true)
            }

          }
          steps {
            sh '''
                    ./jenkins/build/mvn.sh mvn -B -DskipTests clean package
                    ./jenkins/build/build.sh

                '''
          }
        }

        stage('') {
          steps {
            echo 'Hello Mukesh'
          }
        }

      }
    }

    stage('Test') {
      post {
        always {
          junit 'java-app/target/surefire-reports/*.xml'
        }

      }
      steps {
        sh './jenkins/test/mvn.sh mvn test'
      }
    }

    stage('Push') {
      steps {
        sh './jenkins/push/push.sh'
      }
    }

    stage('Deploy') {
      steps {
        sh './jenkins/deploy/deploy.sh'
      }
    }

  }
}