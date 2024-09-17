import java.nio.file.Files
import java.nio.file.Paths

@NonCPS
def getVersionFromGradle() {
    def buildGradleFile = new File('build.gradle').text
    def versionLine = buildGradleFile.find { it.startsWith('version =') }
    return versionLine?.split('=')?.last()?.trim()?.replace("'", "")
}

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
                    // Memanggil metode @NonCPS
                    def version = getVersionFromGradle()
                    env.VERSION = version
                    echo "Version extracted: ${env.VERSION}"
                }
            }
        }
    }
}
