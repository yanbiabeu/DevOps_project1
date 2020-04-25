pipeline {
      agent any
       tools {
        maven 'M2_HOME'
          }
            stages {
             stage ( 'pull repositry') {
                steps {
                echo "pull code from Github"
                git 'https://github.com/yanbiabeu/holliday.git'
                }
                     }
             stage ('build') {
                  steps {
                      echo "Build Step"
                      sh 'mvn clean'
                      sh 'mvn install'
                      sh 'mvn package'
                  }
     
              }
              stage ('test') {
                steps{
                echo "test steps"
                sh "mvn test"
                }
             }   
              stage ('deploy'){
                steps {
                echo "deploy war file"
                sshPublisher(publishers: [sshPublisherDesc(configName: 'Docker-host', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'docker rmi hollidays:1.0; docker build -t hollidays:1.0 .;docker tag hollidays:1.0 epalleewane/hollidays:1.0; docker push epalleewanehollidays:1.0', flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '/webapp/target', sourceFiles: '**/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                }
              }       
                 }
  
     }


