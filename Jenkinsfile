stage('Deploy to Kubernetes') {
    steps {
        script {
            // Cria kubeconfig temporário no workspace
            writeFile file: 'kubeconfig', text: """
apiVersion: v1
kind: Config
clusters:
- cluster:
    server: https://<IP_DO_CLUSTER>:6443
    insecure-skip-tls-verify: true
  name: jenkins-cluster
contexts:
- context:
    cluster: jenkins-cluster
    user: jenkins-user
  name: jenkins-context
current-context: jenkins-context
users:
- name: jenkins-user
  user:
    token: ${credentials('jenkins-k8s-token')}
"""

            // Aponta kubectl para esse kubeconfig temporário
            env.KUBECONFIG = "${env.WORKSPACE}/kubeconfig"

            sh '''
                echo ">>> Aplicando manifestos no Kubernetes..."
                kubectl apply -f k8s/deployment.yaml
                kubectl apply -f k8s/service.yaml
            '''
        }
    }
}
