pipeline {
    agent any
      environment{
        NETLIFY_SITE_ID='f3a621bf-52d0-4e16-b27f-984cf5eb5125'
        NETLIFY_AUTH_TOKEN=credentials('netlify-token')
      }
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
                
                
                 node_modules/.bin/netlify --version
                 echo "Deploy project in $NETLIFY_SITE_ID"
                   node_modules/.bin/netlify status
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
