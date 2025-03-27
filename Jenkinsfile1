node {

def codePath = '/home/test-nodejs/test-nodejs-app/'

        stage('checkout'){
           checkout scm
        }

        withCredentials( [usernamePassword( credentialsId: 'ssh-server', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')])
     {
           def remote = [:]
           remote.name = 'ubuntu-test'
           remote.host = "139.59.76.123"
           remote.user = "${USERNAME}"
           remote.password = "${PASSWORD}"
           remote.allowAnyHosts = true

	stage('Build and Run'){
           sshCommand remote: remote, command: "cd ${codePath}; git pull"
           sshCommand remote: remote, command: "cd ${codePath}; docker build . -f docker/Dockerfile -t node-image:v${env.BUILD_ID}"
           sshCommand remote: remote, command: "cd ${codePath}; docker images"
           sshCommand remote: remote, command: "cd ${codePath}/docker; docker-compose down"
           sshCommand remote: remote, command: "cd ${codePath}/docker; cp docker-compose.yml docker-compose.yml_old"
           previous = sshCommand remote: remote, command: "cd ${codePath}/docker; cat docker-compose.yml | grep -o ':v.*' | sed 's/://g' ", returnStdout: true
           sshCommand remote: remote, command: "cd ${codePath}/docker; sed -i 's/${previous}/v${env.BUILD_ID}/g' docker-compose.yml"
           sshCommand remote: remote, command: "cd ${codePath}/docker; docker-compose up -d"
           }
        }
      }


