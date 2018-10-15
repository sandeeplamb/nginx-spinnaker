pipeline {
    agent  any
    stages {
        stage('Git-Clone') {
            steps {
                sh 'echo "Cloning ...!" '
                sh 'git clone https://github.com/sandeeplamb/nginx-spinnaker.git .'
            }
        }
        stage ('Terraform-Validate') {
            steps {
                sh 'echo "Validating & Copying State..." '
                }
        }
        stage ('Terraform-Plan') {
            steps {
                sh 'echo "terraform plan.." '
            }
        }
        stage ('Terraform-Approve') {
            steps {
                sh 'echo "Approve the Infrastructure."'
                input "Deploy to prod?"
            }
        }
        stage ('Terraform-Apply'){
            steps {
                sh 'echo "terraform apply"'
            }
        }
        stage ('Terraform-State-Save'){
            steps {
                sh 'echo "terraform Push State-File"'
            }
        }
    }
}
