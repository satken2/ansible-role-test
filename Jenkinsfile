pipeline {
  agent {
    docker {
      image 'quay.io/ansible/molecule'
      args '-v /var/run/docker.sock:/var/run/docker.sock'
    }
  }

  stages {
    stage ('対象のブランチにチェックアウト') {
      steps {
        git branch: targetBranch, 
            url: 'https://github.com/satken2/ansible-role-test.git'
      }
    }

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