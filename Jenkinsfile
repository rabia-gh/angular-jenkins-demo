node {
    stage('Checkout') {
        checkout scm
    }
    stage('Build') {
        docker.image('trion/ng-cli').inside {
            bat 'npm install'
            bat 'ng build --progress false --prod --aot'
            bat 'tar -cvzf dist.tar.gz --strip-components=1 dist'
        }
        archive 'dist.tar.gz'
    }
    stage('Test') {
        docker.image('trion/ng-cli-karma').inside {
            bat 'ng test --progress false --watch false'
        }
        junit '**/test-results.xml'
    }
}
