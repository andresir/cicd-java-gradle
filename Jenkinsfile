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
                    def buildGradleFile = new File('build.gradle').readLines()
                    buildGradleFile.each { line ->
                        echo "Line aaaaaaa ====>> : ${line}"
                    }
                    // Membaca file build.gradle dan mendapatkan versi
                    def buildGradleFile = readFile('build.gradle')
                    def versionLine = buildGradleFile.find { it.startsWith('') }
                    def version = versionLine?.split('=')?.last()?.trim()?.replace("'", "")

                    echo "Version buildGradleFile-nyaa: ${buildGradleFile}"
                    echo "Version versionLine-nyaa: ${versionLine}"
                    echo "Version persiii-nyaa: ${version}"
                    
                    // Menyimpan versi sebagai variabel lingkungan
                    env.VERSION = version
                    echo "Version extracted: ${env.VERSION}"
                }
            }
        }
    }
}
