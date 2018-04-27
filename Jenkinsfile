node {
  try {
    stage('Checkout') {
      checkout scm
    }
    stage('Environment') {
      sh 'git --version'
      echo "Branch: ${env.BRANCH_NAME}"
      sh 'docker -v'
      sh 'printenv'
    }
    stage('Build Docker test'){
      sh 'docker build -t jay-react-app -f Dockerfile.test --no-cache . '
    }
    stage('Docker test'){
      sh 'docker run --rm jay-react-app'
    }
    stage('Clean Docker test'){
      sh 'docker rmi jay-react-app'
    }
    stage('Deploy'){
      if(env.BRANCH_NAME == 'master'){
        sh 'docker build -t jay-react-app --no-cache .'
        sh 'docker tag jay-react-app localhost:5000/jay-react-app'
        sh 'docker push localhost:5000/jay-react-app'
        sh 'docker rmi -f jay-react-app localhost:5000/jay-react-app'
      }
    }
  }
  catch (err) {
    throw err
  }
}
