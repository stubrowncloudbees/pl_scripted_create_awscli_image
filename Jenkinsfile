def label = "awscli_image-${UUID.randomUUID().toString()}"
def image_name = "stuartcbrown/awscli:pl_scripted_create_${label}"
podTemplate(label: label,
        containers: [
            containerTemplate(name: 'docker', image: 'docker:17.12.1-ce-dind', privileged: true)
            ]
        ) {
    node(label) {
        container("docker") {
            stage("docker") {
                checkout scm
                echo image_name
                withCredentials([usernamePassword(credentialsId: 'dockerhubstu', passwordVariable: 'PASSWORD', usernameVariable: 'USER')]) {


                    sh 'docker login -p ${PASSWORD} -u ${USER}'
                    sh "docker build . -t $image_name -t stuartcbrown/awscli:latest"

                    sh "docker push $image_name && docker push stuartcbrown/awscli:latest"

                }
            }
        }
    }
}

