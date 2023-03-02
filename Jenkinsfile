pipeline {
  agent {
    docker {
      image 'node:16'
      args '-v /home/ec2-user/.npmrc:/home/node/.npmrc:ro'
    }
  }

  stages {
    stage('Publish') {
      when { branch 'main' }
      steps {
        sh '''
          BASEVERSION=`node -e "var pjson = require('./package.json'); console.log(pjson.version);" | cut -d"." -f1,2`
          npm version "$BASEVERSION.$BUILD_NUMBER"
          npm publish --no-git-tag-version
          '''
      }
    }
  }
}
