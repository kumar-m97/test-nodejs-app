pipeline {
    agent any 
    
    stages {
        stage(checkout){
           steps{
	      git branch: 'master', credentialsId: 'kumar-server', url: 'https://github.com/kumar-m97/test-nodejs-app.git'
	   }
           
	}
        
        stage(Remote Login){
           def remote = [:]
           remote.name = 'ubuntu-test'
           remote.host = '139.59.76.123'
           remote.user = 'root'
           remote.password = 'focus@7045Rite'
           remote.allowAnyHosts = true
           
           steps{
           sshCommand remote: remote, command: "cd /home/test-nodejs/test-nodejs-app"
           sshCommand remote: remote, command: "git pull"
           sshCommand remote: remote, command: "docker build . -f docker/Dockerfile -t node-image:v${env.BUILD_ID}"
           sshCommand remote: remote, command: "docker images"
           sshCommand remote: remote, command: "cd docker"
           sshCommand remote: remote, command: "docker-compose down"
           sshCommand remote: remote, command: "cp docker-compose.yml docker-compose.yml_old"
           previous = sshCommand remote: remote, command: "cat docker-compose.yml | grep -o ':v.*' | sed 's/://g' ", returnStdout: true
           sshCommand remote: remote, command: "sed -i 's/${previous}/v${env.BUILD_ID}/g' docker-compose.yml"
           sshCommand remote: remote, command: "docker-compose up -d"
	   }
	}

    }	


}

/*just for referance

 environment { 
                AN_ACCESS_KEY = credentials('my-predefined-secret-text') 
            }


    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }

tools {
        maven 'apache-maven-3.0.1' 
    }

input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }

stage('Example Deploy') {
            when {
                branch 'production'
            }*/
