pipeline {
    agent any 

    tools {
        nodejs 'nodejs 16.16.0'
    }
    stages {
        stage('SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/akshay0095/react-todo-app.git'
            }
        }
        stage('Install') {
            steps {
                sh 'npm install'
            }

        }
        stage('Build') {
            steps {
                sh 'npm run build'
                fingerprint 'build'
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                rm -rf /var/www/html/*
                mv build/* /var/www/html/
                '''
            }
        }
        stage('Artefact') {
            steps {
                sh 'tar cvzf react_app.tar.gz build/'
                archiveArtifacts artifacts: 'react_app.tar.gz', fingerprint: true, followSymlinks: false, onlyIfSuccessful: true
            }
        }
    }
}
