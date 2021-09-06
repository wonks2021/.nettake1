pipeline {
agent {
    node {
        label 'slave1'
}}
triggers {
    githubPush()    
    }
environment {
dotnet = '/usr/bin/dotnet.exe'
}
stages {
stage ('Checkout') {
            steps {
                //this is a comment 
                git credentialsId: 'userId', url: 'https://github.com/wonks2021/nettake1.git',branch: 'master'
            }
}
stage ('Restore PACKAGES') {     
         steps {
             sh "export PATH=/usr/bin/dotnet:$PATH"
             sh "dotnet restore"
          }
        }
stage('Clean') {
      steps {
            sh 'dotnet clean'
       }
    }
stage('Build') {
     steps {
            sh 'dotnet build'
      }
   }
stage('Pack') {
     steps {
           sh 'dotnet pack --no-build --output nupkgs'
      }
   }
stage('Publish') {
      steps {
           sh "dotnet nuget push **\\nupkgs\\*.nupkg -k yourApiKey -s http://myserver/artifactory/api/nuget/nuget-internal-stable/com/sample"
       }
   }
 }
}
