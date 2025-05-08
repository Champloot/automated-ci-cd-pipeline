pipeline {
  agent any
  stages {
    stage('Deploy') {
      steps {
        sh """
          ssh -o StrictHostKeyChecking=no \
              -i /path/to/ssh/key \
              vagrant@192.168.56.11 \
              'ansible-playbook -i ansible/inventory.ini ansible/deploy-app.yml'
        """
      }
    }
  }
}
