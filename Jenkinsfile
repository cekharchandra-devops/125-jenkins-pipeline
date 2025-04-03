pipeline {
    agent {
        label 'AGENT-1'
    }
    environment {
        MY_ENV_VAR = 'Hello, World!'
    }
    // tools {
    //     maven 'Maven 3.6.3'
    //     jdk 'JDK 11'
    // }
    parameters {
        string(name: 'MY_PARAM', defaultValue: 'default', description: 'A string parameter')
        booleanParam(name: 'MY_BOOLEAN', defaultValue: true, description: 'A boolean parameter')
        choice(name: 'MY_CHOICE', choices: ['Option 1', 'Option 2', 'Option 3'], description: 'A choice parameter')
    }

    // triggers {
    //     cron('H 4 * * 1-5') // Run at 4 AM on weekdays
    //     pollSCM('H/15 * * * *') // Poll SCM every 15 minutes
    //     githubPush() // Trigger on GitHub push events
    /* groovylint-disable-next-line LineLength */
    //     upstream(upstreamProjects: 'my-upstream-job', threshold: hudson.model.Result.SUCCESS) // Trigger on upstream job success
    //     buildTrigger('my-trigger-job') // Trigger another job
    //     buildPipelineTrigger('my-pipeline') // Trigger a downstream pipeline
    //     buildPipelineTrigger('my-pipeline', 'my-branch') // Trigger a specific branch of a downstream pipeline
    //     buildPipelineTrigger('my-pipeline', 'my-branch', 'my-parameters') // Trigger with parameters

    // }
    stages {
        stage('Build') {
            steps {
                retry(3) { // Retry the build stage up to 3 times on failure
                    echo 'Building...'
                    sh exit 1 // Simulate a build failure
                    // Example of using a custom workspace
                    // dir('my-custom-workspace') {
                    //     echo 'Using custom workspace...'
                    //     // Perform actions in the custom workspace
                    // }
                }
                script {
                    // Example of using environment variables and parameters
                    echo "MY_ENV_VAR: ${env.MY_ENV_VAR}"
                    echo "MY_PARAM: ${params.MY_PARAM}"
                    echo "MY_BOOLEAN: ${params.MY_BOOLEAN}"
                    echo "MY_CHOICE: ${params.MY_CHOICE}"
                }
                // Example of using a tool
                // sh 'mvn clean package -Dmaven.test.skip=true' // Skip tests during build
                // Example of using a custom workspace
                // dir('my-custom-workspace') {
                //     echo 'Using custom workspace...'
                //     // Perform actions in the custom workspace
                // }
                // Example of using a Docker agent
                // docker.image('maven:3.6.3-jdk-11').inside {
                //     echo 'Running inside a Docker container...'
                //     // Perform actions inside the Docker container
                // }
                // Example of using a parallel stage
                // parallel(
                //     stage1: {
                //         echo 'Running stage 1...'
                //         // Perform actions for stage 1
                //     },
                //     stage2: {
                //         echo 'Running stage 2...'
                //         // Perform actions for stage 2
                //     }
                // )
                // Example of using a matrix stage
                // matrix {
                //     axes {
                //         axis {
                //             name 'OS'
                //             values 'linux', 'windows'
                //         }
                //         axis {
                //             name 'VERSION'
                //             values '1.0', '2.0'
                //         }
                //     }
                //     stages {
                //         stage('Test') {
                //             steps {
                //                 echo "Testing on ${OS} with version ${VERSION}..."
                //                 // Perform actions for the matrix stage
                //             }
                //         }
                //     }
                // }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
    post {
        always {
            echo 'This will always run after the stages.'
        }
        success {
            echo 'This will run only if the pipeline is successful.'
        }
        failure {
            echo 'This will run only if the pipeline fails.'
        }
    }
    options {
        timestamps()
        timeout(time: 1, unit: 'MINUTES') // Timeout after 1 minute
        // timeout(time: 1, unit: 'MINUTES', message: 'Pipeline timed out') // Custom timeout message
        disableConcurrentBuilds()
        skipDefaultCheckout()
        buildDiscarder(logRotator(numToKeepStr: '5'))
        // lock(resource: 'my-lock') {
        //     echo 'This will run with a lock on the resource.'
        // }

        ansiColor('xterm')
    }
}
