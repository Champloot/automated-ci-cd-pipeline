pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/Champloot/devops_practice.git'
      }
    }
    stage('Deploy') {
      steps {
        sshCommand(
          remote: '192.168.56.11',  // Ansible Controller
          command: """
            cd ${env.WORKSPACE}/ansible &&   // Используем путь из Jenkins workspace
            ansible-playbook -i inventory.ini deploy.yml
          """,
          sshCredentials: [username: 'vagrant', keyFile: '/path/to/ssh-key']
        )
      }
    }
  }
}
