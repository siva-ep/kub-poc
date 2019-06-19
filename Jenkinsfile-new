pipeline
{
    agent any
    stages{
        stage('Clone'){
            steps {
               sh '''
               
               cd /home/reddisekhara_n
               rm -rf front-end-demo
               git clone https://github.com/nagarajui7/front-end-demo.git
               '''
            }
        }
        stage('docker login'){
            steps{
                sh 'sudo docker login --username nagarajubatchu1 --password b@TChU!779263'
            }
        }
        stage('docker image creation'){
            steps{
                sh '''
                cd /home/reddisekhara_n/front-end-demo/
                sudo docker build -t nagarajubatchu1/front-end-1-${BUILD_NUMBER} .
                '''
            }
        }
        stage('docker image push'){
            steps{
                sh 'sudo docker push nagarajubatchu1/front-end-1-${BUILD_NUMBER}'
            }
        }
        stage('kubernetes'){
            steps{
                sh '''
                cd /home/reddisekhara_n/front-end-demo/
                sed -i "s/front-end-1-.*/front-end-1-${BUILD_NUMBER}/g" front-end-deploy-svc.yml
                
                ansible-playbook -i /etc/ansible/hosts deployment.yml
                '''
            }
        }
    }
    
}
