pipeline {
    agent any
    stages {
        stage ('SCM checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ghorpadesaloni/secure_file_transfer_system.git'
            }
        }
        stage ('docker image build') {
            steps {
                sh'/usr/bin/docker image build -t salonighorpade/secure-file-tranfer-image .'
            }
        }
        stage ('docker login') {
            steps {
                sh 'echo dckr_pat_D56b1i2WmP02Q8FkTZa1Jf30bvU | /usr/bin/docker login -u salonighorpade --password-stdin'
            }
        }
        stage ('docker image push') {
            steps {
                sh '/usr/bin/docker image push salonighorpade/secure-file-transfer-image'
            }
        }
        stage ('get the confirmation from user') {
            steps {
                input 'Do you want to deploy this application?'
            }
        }
        stage ('remove existing service') {
            steps {
                sh '/usr/bin/docker service rm service1'
            }
        }
        stage ('create docker service') {
            steps {
                sh '/usr/bin/docker service create --name service1 -p 5000:5000 --replicas 2 salonighorpade/secure-file-transfer-image'
            }
        }
    }
}
