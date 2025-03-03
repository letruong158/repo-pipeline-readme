pipeline {
    agent any
    environment {
        GITHUB_TOKEN = credentials('github-token')
    }
    stages {
        stage('Clean Workspace') {
            steps {
                script {
                    sh 'rm -rf grpc repoc'
                }
            }
        }
        stage('Clone RepoA') {
            steps {
                script {
                    sh '''
                    git config --global credential.helper store
                    echo https://$GITHUB_TOKEN@github.com > ~/.git-credentials
                    git clone https://github.com/letruong158/repoa.git grpc
                    '''
                }
            }
        }
        stage('Generate Doxygen Config') {
            steps {
                script {
                    sh '''
                    doxygen -g Doxyfile
                    echo "INPUT = src" >> Doxyfile
                    echo "GENERATE_HTML = YES" >> Doxyfile
                    echo "WARN_LOGFILE = doxygen_warnings.log" >> Doxyfile
                    '''
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
        stage('Clone RepoC') {
            steps {
                script {
                    sh '''
                    git clone https://github.com/letruong158/repoc.git
                    '''
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    sh '''
                    if [ -f repoc/requirements.txt ]; then
                        pip install -r repoc/requirements.txt
                    fi
                    '''
                }
            }
        }
        stage('Parse Doxygen Warnings') {
            steps {
                script {
                    sh 'python3 repoc/parser.py doxygen_warnings.log'
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
                    archiveArtifacts artifacts: '**/doxygen-output.tar.gz, **/warnings.csv', allowEmptyArchive: true
                }
            }
        }
    }
}