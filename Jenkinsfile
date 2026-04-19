pipeline {
agent any

environment {
    DEPLOY_REPO = "https://github.com/manjukolkar/CD-Project.git"
    BRANCH = "main"
}

stages {

    stage('Checkout Deployment Repo') {
        steps {
            git branch: "${BRANCH}", url: "${DEPLOY_REPO}"
        }
    }

    stage('Deploy to Kubernetes') {
        steps {
            sh '''
            # Apply all manifests
            microk8s kubectl apply -f deployment.yaml
            microk8s kubectl apply -f service.yaml
            microk8s kubectl apply -f ingress.yaml
            '''
        }
    }

    stage('Verify Deployment') {
        steps {
            sh '''
            microk8s kubectl get pods
            microk8s kubectl get svc
            microk8s kubectl get ingress
            '''
        }
    }
}

}
