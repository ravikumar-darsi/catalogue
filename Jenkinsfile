pipeline {
  agent{
    node{
      label 'AGENT-1'
    }
  }
  environment { 
        packageVersion = ''
        nexusURL = '172.31.21.186:8081'
        //http://34.235.126.111:8081/repository/catalogue/
    }
  options {
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()
    }
  // parameters {
  //       // string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

  //       // text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

  //       //booleanParam(name: 'Deploy', defaultValue: false, description: 'Toggle this value')

  //       // choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

  //       // password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
  //   }
  stages{
    stage('Get the Version') {
        steps {
                script { // def means creation of variable
                    def packageJson = readJSON file: 'package.json'
                    packageVersion = packageJson.version
                    echo "application version: $packageVersion"
                }
            }
    }
    stage('Install dependencies') {
            steps {
                sh """
                    npm install
                """
            }
        }
        stage('Unit tests') {
            steps {
                sh """
                    echo "unit tests will run here"
                """
            }
        }
         stage('Build') {
            steps {
                sh """
                    ls -la
                    zip -q -r catalogue.zip ./* -x ".git" -x "*.zip"
                    ls -ltr
                """
            }
        }
        stage('Publish Artifact') {
            steps {
                 nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: "${nexusURL}",
                    groupId: 'com.roboshop',
                    version: "${packageVersion}",
                    repository: 'catalogue',
                    credentialsId: 'nexus-auth',
                    artifacts: [
                        [artifactId: 'catalogue',
                        classifier: '',
                        file: 'catalogue.zip',
                        type: 'zip']
                    ]
                )
            }
        }
  }
  post {
     always {
          echo 'I will always say Hello again!..'
          deleteDir()
        }
     failure {
          echo 'This block of scripts runs only when pipeline is failed, used generally to send some alerts'
        }
     success {
          echo 'I will say Hello when pipeline is executed successfully'
        }
  }
}