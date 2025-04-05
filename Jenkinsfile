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
               sh '''
               ssh -o StrictHostKeyChecking=no root@${SERVER_IP} << 'ENDSSH'
               hostname
               echo "Deployment is in Progress"
               cd /home/ubuntu/test-nodejs-app
               pwd
               git pull
               pm2 stop ${NODE_PROCESS_NAME} || true
               npm install --production
               npm run build
               pm2 start ${NODE_PROCESS_NAME}
               echo "Deployment successful!"
               ENDSSH
            '''
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
