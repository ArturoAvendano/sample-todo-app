pipeline {
    agent any
    environment {
        LT_BUILD_NAME = "lambdatest-pipeline"
    }
    stages {
  stage('Setup') {
    steps {
      sh 'curl https://downloads.lambdatest.com/tunnel/v3/linux/64bit/LT_Linux.zip --output LT_Linux.zip'
      sh 'unzip -o LT_Linux.zip'
      sh './LT --user ${LT_USERNAME} --key ${LT_ACCESS_KEY} --tunnelName jenkins-tunnel --infoAPIPort 8000 &'
    }
  }
  stage('Test') {
    steps {
      sh 'sleep 5' 
      sh 'python3 -m http.server 8081 &'
      sh 'python3 test_sample_todo_app.py'
      sh 'pkill -f "http.server"'
      sh 'sleep 10'
      sh 'curl -X DELETE http://127.0.0.1:8000/api/v1.0/stop' 
    }
  }

}
}
