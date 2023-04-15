pipeline {
    agent any

    environment {
            // ENV_URL = "pipeline.global.com"  //declaring at pipeline will allow all stages to access this cvariable
            SSH_CRED = credentials('SSH_CRED')
        }
    stages {
        stage('lint checks') {  
            when { branch pattern: "feature-.*", comparator: "REGEXP" }
             steps {
                sh "env"
                sh "echo runs only on feature branch"
                // sh "ansible-playbook -e ansible_user=${SSH_CRED_USR} -e ansible_password=${SSH_CRED_PSW} -e COMPONENT=Mongodb -e ENV=dev robot-dryrun.yml"
            }
        }

        stage('PR for dry run') {
            when { branch pattern: "PR-.*", comparator: "REGEXP" }
             steps {
                sh "env"
                sh "echo runs only on feature branch"
                sh "ansible-playbook -e ansible_user=${SSH_CRED_USR} -e ansible_password=${SSH_CRED_PSW} -e COMPONENT=Mongodb -e ENV=dev robot-dryrun.yml"
            }
        }

        stage('main') {  
            when { branch 'main' }
             steps {
                sh "env"
                sh "echo runs only on main branch"
                // sh "ansible-playbook -e ansible_user=${SSH_CRED_USR} -e ansible_password=${SSH_CRED_PSW} -e COMPONENT=Mongodb -e ENV=dev robot-dryrun.yml"
            }
        }

        stage('runs against tags') {  
            when { expression { env.TAG_NAME ==~ ".*" } }  // we can use this if we dont know pattern of tags
             steps {
                sh "env"
                sh "echo $TAG_NAME"
                // sh "ansible-playbook -e ansible_user=${SSH_CRED_USR} -e ansible_password=${SSH_CRED_PSW} -e COMPONENT=Mongodb -e ENV=dev robot-dryrun.yml"
            }
        }

        }

    }
//testing on different branch