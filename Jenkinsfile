void setBuildStatus(String message, String state) {
  step([
    $class: "GitHubCommitStatusSetter",
    reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/satken2/ansible-role-test.git"],
    contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "Ansible-Molecule"],
    errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
    statusResultSource: [ $class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]] ]
  ]);
}

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
  // 実行結果に応じてGitLabのコミットステータスを変更する
  post {
    success {
      echo "SUCCESS"
      setBuildStatus("AnsibleチェックOK", "SUCCESS");
    }
    failure{
      echo "failure"
      setBuildStatus("AnsibleチェックNG", "FAIL");
    }
  }
}