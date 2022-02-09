node{
    stage('SCM Checkout'){
            dir("$JENKINS_HOME/jobs/$JOB_NAME/workspace/$BUILD_NUMBER"){
                     git branch: 'dev', credentialsId: 'gitCredentials ', url: 'http://10.143.140.124/root/apim_apigw.git' 
            }
    }
    stage('Docker File Creation'){
            dir("$JENKINS_HOME/jobs/$JOB_NAME/workspace/$BUILD_NUMBER"){
                sh '''
                 
                          ls *.zip | echo -e FROM 10.143.140.124:5010/apim-sag-apigw-ext:v1.4 \'\n\'COPY $(cat -) opt/softwareag/IntegrationServer/instances/default/replicate/inbound/ > Dockerfile
                '''
            }
    }
    stage('Docker Build'){
           dir("$JENKINS_HOME/jobs/$JOB_NAME/workspace/$BUILD_NUMBER"){
                 sh ''' 
                         sudo docker build -t 10.143.140.124:5010/apim-sag-apigw-ext-$BUILD_NUMBER .
                '''
           }
          
    }
     stage('Docker Image Upload'){
         sh '''
             sudo docker push 10.143.140.124:5010/apim-sag-apigw-ext-$BUILD_NUMBER
          '''
    }
   
}

