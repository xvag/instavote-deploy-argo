pipeline {

  agent {
    kubernetes {
      yamlFile 'build-agent.yaml'
      defaultContainer 'jnlp'
      idleMinutes 1
    }
  }

  stages {
    stage('Daily Compliance Run') {
      steps{
        container('jnlp') {
          echo 'Running a compliance scan with inspec....'
            script{
              def remote = [:]
              remote.name = "controlnode"
              remote.host = "104.199.83.161"
              remote.allowAnyHosts = true

              withCredentials([sshUserPrivateKey(credentialsId: 'sshUser', keyFileVariable: 'identity', passphraseVariable: '', usernameVariable: 'userName')]) {
                  remote.user = userName
                  remote.identityFile = identity
                  stage("Placeholder Stage...") {
                    sshCommand remote: remote, sudo: true, command: 'echo "add your stuff here....."'
                    sshCommand remote: remote, sudo: true, command: 'echo "some more stuff goes here....."'
                }
                  stage("Scan with InSpec") {
                    sshCommand remote: remote, sudo: true, command: 'inspec exec /root/linux-baseline/'
                }
              }
            }
          }
      }
    }
  }
}
