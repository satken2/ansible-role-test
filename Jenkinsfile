pipeline {
  agent {
    docker {
      image 'quay.io/ansible/molecule'
      args '-v /var/run/docker.sock:/var/run/docker.sock'
    }
  }

  stages {
    stage ('バージョンの表示') {
      steps {
        sh '''
          docker -v
          python -V
          ansible --version
          molecule --version
        '''
      }
    }

    stage ('Moleculeテスト実行') {
      steps {
        sh 'molecule test --all'
      }
    }
    
  }
}