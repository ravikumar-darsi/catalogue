pipeline {
    agent {
        node {
            label 'AGENT-1' // Specifies the node with label 'AGENT-1' to run the pipeline on
        }
    }
    environment { 
        packageVersion = '' // Placeholder for the package version extracted from the package.json file
        nexusURL = '172.31.21.186:8081' // URL for Nexus repository
    }
    options {
        timeout(time: 1, unit: 'HOURS') // Set timeout of 1 hour for the entire pipeline
        disableConcurrentBuilds() // Prevents concurrent builds of the same job
    }

    // Uncomment the parameters block if you need to pass parameters
    //  parameters {
    // //     string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
    // //     text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
    //        booleanParam(name: 'Deploy', defaultValue: false, description: 'Toggle this value')
    // //     choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
    // //     password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    //  }

    stages {
        stage('Get the Version') {
            steps {
                script {
                    // Read the version from the package.json file
                    //def is used to declare variables in groovy script
                    def packageJson = readJSON file: 'package.json'
                    packageVersion = packageJson.version // Set packageVersion to the version in package.json
                    echo "application version: $packageVersion" // Display the version in the console output
                }
            }
        }
      }
    post {
        always {
            echo 'I will always say Hello again!..' // This will always run, regardless of the build result
            deleteDir() // Clean up workspace after the build
        }
        failure {
            echo 'This block of scripts runs only when the pipeline has failed, used generally to send some alerts' // Execute only on failure
        }
        success {
            echo 'I will say Hello when the pipeline is executed successfully' // Execute only on successful execution
        }
    }
}