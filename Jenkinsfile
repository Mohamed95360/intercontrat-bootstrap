pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'dotnet build bootstrap.sln'
      }
    }

    stage('unit') {
      parallel {
        stage('unit') {
          steps {
            sh 'dotnet test tests/UnitTests'
          }
        }

        stage('integration') {
          steps {
            sh 'dotnet test tests/IntegrationTests'
          }
        }

        stage('function') {
          steps {
            sh 'dotnet test tests/FunctionalTests'
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        sh 'dotnet publish bootstrap.sln -o /var/aspnet'
      }
    }

  }
}