pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
               checkout([$class: 'GitSCM', branches: [[name: '**']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/igortchatcho/my_Ec2']]])
            }
        }
        
        stage('terraform init') {
            steps {
                sh ('terraform init');
            }
        }
        
        stage('terraform fmt') {
            steps {
                sh ('terraform fmt');
            }
        }
        
        stage('terraform validate') {
            steps {script{
            sh '''
                c=$(echo $/)
                echo $c
                if [ $c == 0 ]
                then
                  echo "the configuration file is valid"
                else
                  echo "your configuration file is not valid"
                fi    ''';
            }
        }}
        
        stage('terraform plan') {
            steps {
                sh ('terraform plan');
            }
        }
        
        stage('terraform apply') {
            steps {
                sh 'terraform apply --auto-approve'
            }
        }    
    }
}
