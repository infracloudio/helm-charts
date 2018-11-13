node{
    stage('Helm Init'){
        sh "echo $_imagetag"
        tagValue = _imagetag.split('-')[0]
        envType = ""
        if (tagValue == "dev") {
            envType = "dev-manifold"
        } else if (tagValue == "qa") {
            envType = "qa-manifold"
        }
        
        stage('Deploy Chart'){
             if (envType) {
                sh "helm status ${tagValue}-alpine 2>/dev/null || helm install https://infracloudio.github.io/helm-charts/charts/alpine-0.1.0.tgz -f https://infracloudio.github.io/helm-charts/alpine/${tagValue}-values.yaml --set image.tag=${_imagetag} --name ${tagValue}-alpine --namespace ${envType} --dry-run --debug"
                sh "helm upgrade ${tagValue}-alpine  https://infracloudio.github.io/helm-charts/charts/alpine-0.1.0.tgz -f https://infracloudio.github.io/helm-charts/alpine/${tagValue}-values.yaml --set image.tag=$_imagetag --namespace ${envType} --dry-run --debug"
            }
        }
    }
}
