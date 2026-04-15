pipeline {
    agent any

    tools {
        // Name must match Manage Jenkins -> Tools -> JDK
        jdk 'JDK'
        // Name must match Manage Jenkins -> Tools -> Gradle
        gradle 'Gradle' 
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/CyberBrain18/MyMavenToGradle.git'
            }
        }

        stage('Build & Test') {
            steps {
                // Since we aren't using the wrapper (./gradlew), 
                // we call 'gradle' directly. 
                // Jenkins will use the version defined in the 'tools' block.
                sh 'gradle clean build'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: Project built using Global Gradle installation!'
        }
        failure {
            echo 'FAILURE: Verify that "Gradle" is configured in Jenkins Global Tool Configuration.'
        }
    }
}
