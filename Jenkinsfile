podTemplate(label: 'android', namespace: 'natsukikana', containers: [
    containerTemplate(name: 'docker-android', image: 'docker-android:latest', ttyEnabled: true)
  ]) {
    node('android') {
        container('docker-android') {
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
                sh 'npm run build-android-bundle'
            }
            stage('Build - npm bundle') {
                dir('android'){
                    sh 'gradle clean assembleDebug'
                }
            }
           stage('archive'){
               archiveArtifacts 'android/app/build/outputs/apk/*.apk'
           }
        }
    }
}
