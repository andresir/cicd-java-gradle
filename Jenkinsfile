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
                    // Membaca file build.gradle dan mendapatkan versi
                    def buildGradleFile = readFile('build.gradle')
                    // def versionLine = buildGradleFile.find { it.startsWith('version =') }
                    def versionLine = buildGradleFile.find { it.trim().startsWith('version =') }
                    def version = versionLine?.split('=')?.last()?.trim()?.replace("'", "")

                    echo "Version buildGradleFile-nyaa: ${buildGradleFile}"
                    echo "Version versionLine-nyaa: ${versionLine}"
                    echo "Version persiii-nyaa: ${version}"
                    
                    // Menyimpan versi sebagai variabel lingkungan
                    env.VERSION = version
                    echo "Version extracted: ${env.VERSION}"

                    // Cara Lain
                    def buildGradleFilex = new File('build.gradle').readLines()
                    def versionLinex = buildGradleFilex.find { it.trim().startsWith('version =') }
                    if (versionLinex) {
                        def versionx = versionLinex.split('=')?.last()?.trim()?.replaceAll("[\'\"].*", "")
                        echo "Version extracted-222222: ${versionx}"
                    } else {
                        echo "Version line not found xxxxxxxxxxxx."
                    }
                }
            }
        }
    }
}
