pipeline {
 agent none
 stages {
  stage('Run Command') {
   agent {
    label 'Mac'
   }
   sh 'node --version'
   sh 'gradle -v'
   sh 'hostname -f'
  }
  stage('Build - check out & install') {
   agent {
    label 'Mac'
   }
   checkout scm
   sh 'npm install'
  }
  stage('Build - npm bundle') {
   agent {
    label 'Mac'
   }
   sh 'mkdir -p android/app/src/main/assets/'
   sh 'npm run build-android-bundle'
  }
  stage('Build - npm bundle') {
   agent {
    label 'Mac'
   }
   sh 'cd android && gradle clean assembleDebug'
  }
  stage('archive') {
   agent {
    label 'Mac'
   }
   archiveArtifacts 'android/app/build/outputs/apk/*.apk'
  }
 }
}
