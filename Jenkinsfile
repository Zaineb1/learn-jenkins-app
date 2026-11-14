pipeline {
    agent any

    stages {
        stage('build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
               sh '''
                
                  node --version
               
               '''
            }
        }
        stage('Test'){
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                test -f build/index.html
                npm test
                '''
                
            }
        }
       
        
        stage('deploy') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
               sh '''
                
                 npm install netlify-cli
                 node_modules/.bin/netlify --version
               
               '''
            }
        }

    }
    post{
        always{
            junit 'test-results/junit.xml'
        }
    }
}
