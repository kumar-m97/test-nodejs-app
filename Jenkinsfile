pipeline {
   agent any
   environment {
      SERVER_IP = '3.83.179.185'
      APP_DIR = '/home/ubuntu/test-nodejs-app'
      NODE_PROCESS_NAME = 'nodejs-app'
   }
   stages {
      stage ('Deploy App') {
         steps {
            sshagent(credentials: ['app-ssh-key']){
               sh """
                  ssh -o StrictHostKeyChecking=no root@${SERVER_IP} '
                     hostname
                     echo "Deployment is in Progress"
                     cd /home/ubuntu/test-nodejs-app
                     pwd
                     git pull
                     pm2 stop nodejs-app
                     npm install
                     pm2 start nodejs-app
                     echo "Deployment successful!"
                  '
               """
            }
         }
      }
   }
   post {
      always {
         echo 'This pipeline was run'
      }
   } 
}
