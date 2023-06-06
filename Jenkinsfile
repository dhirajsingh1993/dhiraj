library 'reference-pipeline'
pipeline {  agent {    docker {    label 'docker'    image '    args '-u root:root'    }  }
  parameters {    choice(name: 'CF_ENV', choices: 'UAT', description: 'Target Environment')  }
  options {    buildDiscarder(logRotator(numToKeepStr: '10'))  }
  tools {    jdk 'JAVA_8'  }
  stages {
    stage('Validate Commit') {      // when {      //   anyOf {      //     environment name: 'CF_ENV', value: 'development'      //     branch 'development'      //   }      //   not {      //     anyOf {      //       environment name: 'CF_ENV', value: 'release'      //       environment name: 'CF_ENV', value: 'staging'      //       environment name: 'CF_ENV', value: 'production'      //     }      //   }      // }      steps {        echo("Test committed source on Saleforce Sandbox")          withCredentials([sshUserPrivateKey(credentialsId: 'CED_UAT', keyFileVariable: 'CED_SERVER_KEY', passphraseVariable: 'CED_CLIENT_ID', usernameVariable: 'CED_USER')]) {          sh '''            pwd            ls -ltra            chmod 0777 /            ./ci-sandbox.sh          '''        }      }    }  }}
