pipeline {
    agent any
    environment {
        VERSION = ''
    }
    stages {
        stage('Checkout') {
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/andresir/cicd-java-gradle.git']]])
            }
        }
        stage('check Version') {
            steps {
                script {
                    // // Membaca file build.gradle dan mendapatkan versi
                    // def buildGradleFile = readFile('build.gradle')
                    // echo "File content:\n${buildGradleFile}.take(100)"
                    // // def baris = buildGradleFile.each { line ->
                    // //     echo "Line: ${line}" }
                    // def versionLine = buildGradleFile.find { it.startsWith('p') }
                    // def version = versionLine?.split('=')?.last()?.trim()?.replace("'", "")

                    // // echo "barissnyaa ==> ${baris}"
                    // echo "Version buildGradleFile-nyaa: ${buildGradleFile}"
                    // echo "Version versionLine-nyaa: ${versionLine}"
                    // echo "Version persiii-nyaa: ${version}"
                    
                    // // Menyimpan versi sebagai variabel lingkungan
                    // env.VERSION = version
                    // echo "Version extracted: ${env.VERSION}"

                    def xxx = sh(script: "grep -oP \"(?<=version = ')[^']+\" build.gradle", returnStdout: true).trim()
                    sh "echo ${xxx}"
                    def version_value = sh(returnStdout: true, script: "cat build.gradle | grep -o 'version = [^,]*'").trim()
                    sh "echo Project in version value: $version_value"
                    def version = version_value.split(/=/)[1].trim()
                    sh "echo final version: $version"
                    env.VERSION = version
                    sh "echo ENV version: ${env.VERSION}"
                }
            }
        }
        stage('Get Version from env') {
            steps {
                script {
                    sh "echo version from env: ${env.VERSION}"
                }
            }
        }
    }
}
