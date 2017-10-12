pipeline {
    agent "Mac" {
            stages {
        stage('Run Command') {
            print 'in side node'
            sh 'node --version'
            sh 'gradle -v'
            sh 'hostname -f'
        }
        stage('Build - check out & install') {
            checkout scm
            sh 'npm install'
        }
        stage('Build - npm bundle') {
            sh 'mkdir -p android/app/src/main/assets/'
            sh 'npm run build-android-bundle'
        }
        stage('Build - npm bundle') {
            sh 'cd android && gradle clean assembleDebug'
        }
       stage('archive'){
           archiveArtifacts 'android/app/build/outputs/apk/*.apk'
       }
    }
    }
}
