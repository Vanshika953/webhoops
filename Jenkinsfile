node {
    stage('Checkout Code') {
        git branch: 'main',
            url: 'https://github.com/Vanshika953/webhoops.git',
            credentialsId: 'github-creds'
    }

    stage('SonarQube Analysis') {
        withSonarQubeEnv('sonar-server') {
            sh '''
              sonar-scanner \
              -Dsonar.projectKey=webhoops \
              -Dsonar.projectName=webhoops \
              -Dsonar.sources=.
            '''
        }
    }

    stage('Quality Gate') {
        timeout(time: 5, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
        }
    }

    stage('Deploy') {
        echo "Deploying application..."
    }
}
