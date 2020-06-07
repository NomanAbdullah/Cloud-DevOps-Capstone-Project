pipeline {
	agent any
	stages {

		stage('Stage 1 - Creating Kubernetes Cluster') {
			steps {
				withAWS(region:'us-east-1', credentials:'eks_cred') {
					sh '''
						eksctl create cluster \
						--name capstonecluster \
						--version 1.16 \
						--nodegroup-name standard-workers \
						--node-type t2.small \
						--nodes 2 \
						--nodes-min 1 \
						--nodes-max 3 \
						--node-ami auto \
						--region us-east-1 \
						--zones us-east-1a \
						--zones us-east-1b \
						--zones us-east-1c \
					'''
				}
			}
		}

		

		stage('Stage 2 - Creating a Conf file Cluster') {
			steps {
				withAWS(region:'us-east-1', credentials:'eks_cred') {
					sh '''
						aws eks --region us-east-1 update-kubeconfig --name capstonecluster
					'''
				}
			}
		}

	}
}
