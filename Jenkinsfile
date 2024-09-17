pipeline {
    agent any
    environment {
        VERSION = 'my-version'
    }
    stages {
        stage('Checkout') {
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/andresir/cicd-java-gradle.git']]])
            }
        }
        stage('Get Version') {
            steps {
                script {
                    def buildGradleFile = readFile('build.gradle')
                    def versionLine = buildGradleFile.find { it.startsWith('version =') }
                    def version = versionLine?.split('=')?.last()?.trim()?.replace("'", "")

                    env.VERSION = version
                    echo "Version extracted: ${env.VERSION}"
                }
            }
        }
    }
}
