pipeline {
 agent {
  label 'Mac'
 }
 stages {
  stage('Run Command') {
   steps {
    sh 'node --version'
    sh 'gradle -v'
    sh 'hostname -f'
   }
  }
  stage('Build - check out & install') {
   steps {
    checkout scm
    sh 'npm install'
   }
  }
  stage('Build - npm bundle') {
   steps {
    sh 'mkdir -p android/app/src/main/assets/'
    sh 'npm run build-android-bundle'
   }
  }
  stage('Build - npm bundle') {
   steps {
    sh 'cd android && gradle clean assembleDebug'
   }
  }
  stage('archive') {
   steps {
    archiveArtifacts 'android/app/build/outputs/apk/*.apk'
   }
  }
 }
}
