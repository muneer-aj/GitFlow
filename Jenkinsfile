node {  
     stage('Build AngularJS') {
        checkout scm
        sh '''echo "Building AngularJs application....."
echo "$WORKSPACE"
ng build
cd dist
echo "Packaging Angular code"
echo "--------------------------------------------------"
jar -cvf DevOpsTools.war *
mv -f DevOpsTools.war $WORKSPACE/DevOpsTools.war
cd $WORKSPACE
ls -ls'''
    }
    stage('Docker Image Creation'){
        build job: '/AngularJS_CreateDockerImage', parameters: [[$class: 'StringParameterValue', name: 'DOCKER_IMAGE_TAG', value: BUILD_NUMBER]]
    }
    stage('Deploy To Environment'){
        build job: '/AngularJS_Deploy', parameters: [[$class: 'StringParameterValue', name: 'DOCKER_IMAGE_TAG', value: BUILD_NUMBER], [$class: 'StringParameterValue', name: 'Environment', value: 'DEV']]
    }
    
}
