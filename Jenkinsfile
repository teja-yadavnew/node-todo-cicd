pipeline{
    agent {label 'teja'}
    
    stages{
        stage('code'){
            steps{
                git url: 'https://github.com/teja-yadavnew/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('build and testing'){
            steps{
                sh 'docker build . -t velpulateja1998701/node-todo-app-cicd:latest'
            }
        }
           stage('login and push image'){
            steps{
                echo "logining into docker hub and pushing image.."
                withCredentials([usernamePassword(credentialsId:'dockerhub',passwordVariable:'dockerhubPassword', usernameVariable:'dockerhubUser')]) {
                    sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPassword}"
                    sh "docker push velpulateja1998701/node-todo-app-cicd:latest"
                }
            }
        }
           stage('deploy'){
            steps{
                sh 'docker-compose down && docker-compose up -d'
            }
        }
        
    }
}
