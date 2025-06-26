pipeline {
    agent {label 'server1-farham'}

    stages {
        stage('Pull SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/farhamapple/simple-apps.git'
            }
        }
        
        stage('Build') {
            steps {
                sh'''
                cd apps
                npm install
                '''
            }
        }
        
        stage('Testing') {
            steps {
                sh'''
                cd apps
                npm test
                npm run test:coverage
                '''
            }
        }
        
        stage('Code Review') {
            steps {
                sh'''
                cd apps
                sonar-scanner \
                    -Dsonar.projectKey=simple-apps \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://172.23.14.102:9000 \
                    -Dsonar.login=sqp_f91ce69860b0e7b02999a7ac3cfaf6a50fe37cc3
                '''
            }
        }
        
    }
}