pipeline {
    agent any
    environment {
        GITHUB_TOKEN = credentials('github-token')
    }
    stages {
        stage('Clean Workspace') {
            steps {
                script {
                    sh 'rm -rf grpc'
                }
            }
        }
        stage('Clone RepoA') {
            steps {
                script {
                    sh '''
                    git config --global credential.helper store
                    echo https://$GITHUB_TOKEN@github.com > ~/.git-credentials
                    git clone https://github.com/letruong158/repoa.git
                    '''
                }
            }
        }
        stage('Generate Doxygen Config') {
            steps {
                script {
                    sh 'doxygen -g Doxyfile'
                }
            }
        }
        stage('Run Doxygen') {
            steps {
                script {
                    sh 'doxygen Doxyfile'
                }
            }
        }
        stage('Pack Output') {
            steps {
                script {
                    sh 'tar -czf doxygen-output.tar.gz ./html'
                }
            }
        }
        stage('Archive Artifacts') {
            steps {
                script {
                    archiveArtifacts artifacts: '**/doxygen-output.tar.gz', allowEmptyArchive: true
                }
            }
        }
    }
}