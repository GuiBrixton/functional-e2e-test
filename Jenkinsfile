pipeline{

  agent {
    node {
        label 'jenkins-nodo-java'
    }
  }
  stages {
    stage('Run function testing E2E') {
      steps {
        sh 'mvn clean verify -Dwebdriver.remote.url=https://standalone-chrome:default/wd/hub -Dwebdriver.remote.driver=chrome -Dchrome.switches="--no-sandbox,--ignore-certificate-errors,--homepage=about:blank,--no-first-run,--headless"'
      }
    }

    stage('Generate Cucumber Report') {
      steps {
        sh 'mvn serenity:aggregate'

        publishHTML(target: [
            reportName : 'Serenity',
            reportDir:   'target/site/serenity',
            reportFiles: 'index.html',
            keepAll:     true,
            alwaysLinkToLastBuild: true,
            allowMissing: false
        ])

      }
    }
  }

  post {
    always {
        sh 'docker logout'
    }
  }

}