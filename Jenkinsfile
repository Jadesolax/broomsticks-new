pipeline{
    agent any
    tools {
        nodejs "node"
    }
    stages{
        stage('test'){
            steps{
                echo "Testing stage"
            }
        }

        stage('production'){
            steps{
                sh '''
                    sudo ssh -i /var/lib/jenkins/demo.pem -t -o StrictHostKeyChecking=no ubuntu@ec2-3-10-4-189.eu-west-2.compute.amazonaws.com
                    cd /var/www
                    sudo rm -rf html
                    sudo mkdir html
                    cd html
                    sudo git init
                    sudo git remote add origin https://github.com/cyclobold/broomsticks.git
                    sudo git fetch
                    sudo git checkout with-auth-thoughts
                    sudo git pull origin with-auth-thoughts
                    sudo npm install
                    pm2 kill
                    PORT=3000 pm2 start ./bin/www
                   '''
            }
        }
    }
}