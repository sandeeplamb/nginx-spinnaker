pipeline {
    agent  any
    stages {
        stage('Git-Clone') {
            steps {
                sh 'echo "Cloning ...!" '
                sh 'rm -rf *; rm -rf .git*; rm -rf .terraform'
                sh 'git clone https://github.com/sandeeplamb/Jenkins-Pipeline.git .'
            }
        }
        stage ('Terraform-Validate') {
            steps {
                sh 'echo "Validating & Copying State..." '
                sh 'cp /var/jenkins_home/aws_data/terraform.tfvars terraform/'
                sh 'yes | cp -rf terraform/* /var/jenkins_home/aws_iaas/'
                sh 'cd /var/jenkins_home/aws_iaas/;/var/jenkins_home/.local/bin/aws s3 cp s3://aws-sandbox-poc-gaming ./terraform.tfstate'
                sh 'cd /var/jenkins_home/aws_iaas/;/var/jenkins_home/bin/terraform init;/var/jenkins_home/bin/terraform validate'
            }
        }
        stage ('Terraform-Plan') {
            steps {
                sh 'echo "terraform plan.." '
                sh 'cd /var/jenkins_home/aws_iaas/;/var/jenkins_home/bin/terraform plan'
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
                sh 'cd /var/jenkins_home/aws_iaas/;/var/jenkins_home/bin/terraform apply -auto-approve'
            }
        }
        stage ('Terraform-State-Save'){
            steps {
                sh 'echo "terraform Push State-File"'
                sh 'cd /var/jenkins_home/aws_iaas/;/var/jenkins_home/.local/bin/aws s3 cp terraform.tfstate s3://aws-sandbox-poc-gaming'
            }
        }
    }
}
