pipeline {
    agent any

    triggers {
        pollSCM('*/5 * * * *')
    }

    stages {
        stage('Compile') {
            steps {
                gradlew('clean', 'classes')
            }
        }
        stage('Build') {
            steps {
                gradlew('build')
            }
            post {
                always {
                    junit '**/build/test-results/test/TEST-*.xml'
                }
            }
        }
    }
    post {
        failure {
            mail to: 'chidumekwueme@gmail.com', subject: 'Build failed', body: 'Please fix!'
        }
    }
}

def gradlew(String... args) {
    sh "./gradlew ${args.join(' ')} -s"
}