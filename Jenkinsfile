node('php'){
    stage('Clean'){
        deleteDir()
        sh 'ls -la'
    }
    
    stage('Fetch') {
        checkout scm
    }
    
    stage('Build'){
        sh 'composer install --prefer-dist --no-dev --ignore-platform-reqs'             
    }
  
    stage ('config') {
        paralell(
            'config cache': {
                    sh 'php artisan config:cache'
                },
            'config cache': {
                    sh 'php artisan route:cache'
                }
            
            )    
    }   
    
    stage('Docker Build') {
        sh 'docker build -t fernandorozante2/todoapi:$BUILD_NUMBER .'
    }
    
    stage('Docker Ship') {
        sh 'docker push fernandorozante2/todoapi:$BUILD_NUMBER'
    }
}
