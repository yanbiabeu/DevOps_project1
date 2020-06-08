
pipeline {
    agent any
    triggers {
        cron(' H/1 * * * * ')
     }
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
                sshPublisher(publishers: [sshPublisherDesc(configName: 'Docker-host', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'docker build -t hollidays:v.${BUILD_NUMBER} .; docker tag hollidays:v.${BUILD_NUMBER} eab046/hollidays:v.${BUILD_NUMBER}; docker push eab046/hollidays:v.${BUILD_NUMBER}', flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '/webapp/target', sourceFiles: '**/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                }
              }
              stage ('continuous deployment') {
                steps{
                echo "Deploying to Docker"
                sshPublisher(publishers: [sshPublisherDesc(configName: 'Docker-host', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'docker run -itd --name Devopsdreams -p 8080:8080 eab046/hollidays:v.${BUILD_NUMBER-1}', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                }
             }   
              
           }
  
     }




