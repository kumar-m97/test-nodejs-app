pipeline {
    agent any 
    
    stages {
        stage(checkout){
           steps{
	      checkout scm   
	   }
	}
    }	


}

//just for referance

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
            }
