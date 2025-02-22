node {
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
        stage('Checkout') {
            checkout scm
            sh 'ls -la'
        }
        stage('Build') {
            sh 'npm install'
        }
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
        stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy?', 
                  ok: 'Proceed'
        }
        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            echo "Aplikasi berjalan, menunggu 1 menit..."
            sleep(time: 1, unit: 'MINUTES') 
            sh './jenkins/scripts/kill.sh'
        }
    }
}
