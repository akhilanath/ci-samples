pipeline {
  agent {
    node { label 'katalon' }
}
    
 /*

  environment {
        def readContent = readJSON file: './HsenSimulator-Frontend/devops/env.json'
        componentName = "${readContent['component_name']}"
        projectName = "${readContent['dev_project_name']}"
        apiPath = "${readContent['api_path']}"
        backendApp = "${readContent['backend_app']}"
        builderImage = "modern-webapp:10.x";
        latestTag = "latest";
        buildTag = "Build-${BUILD_NUMBER}";
        releaseTag = "qa";
        expSqdTag = "es-poc";
        kafkatemplatename = "kafka";
        language = "java";
        projectkey = "testkey";
        APPLITOOLS_API_KEY='9YKGkLEvsFsovZlE506nUgTLEcYU110j5AYwm1103MNbAco110'
  }
  */
  stages {
        stage('Test') {
            steps {
            //git branch: 'master',
            //    url: 'https://github.com/katalon-studio-samples/ci-samples.git'
                sh ' -browserType="Chrome" -retry=0 -statusDelay=15 -testSuitePath="Test Suites/TS_RegressionTest"'
            }
    
    post {
        always {
            archiveArtifacts artifacts: 'report/**/*.*', fingerprint: true
            junit 'report/**/JUnit_Report.xml'
        }
    }
}
  
  
  
  
  
  
  
  
  
  
  
/*
  stages {
   stage ('Install NPM modules'){
      steps{
        script{
           sh "npm install"
        }
      }
    }
    */
    
 /*   stage('Create Image') {
            agent { 
        label 'maven'
        }

    
    
      steps {
      dir("HsenSimulator-Frontend") {
        script {
          withCredentials([string(credentialsId: "${JENKINS_SA}", variable: 'TOKEN')]) {
            def check_bc = sh (
                script: "oc --token=${TOKEN} get bc -n ${env.projectName} | grep ${env.componentName} | awk '{print \$1}'",
                returnStdout: true
                )
            if(check_bc.contains("${env.componentName}")) {
             sh "oc --token=${TOKEN} start-build ${env.componentName} --from-dir=. -n ${env.projectName} --wait"
            }
            else{
             sh "oc --token=${TOKEN} new-build --binary --image-stream ${env.builderImage} -e OUTPUT_DIR=dist/hsenSimulator -e YARN_ENABLED=true --name ${env.componentName} -n ${env.projectName}"
             sh "oc --token=${TOKEN} start-build ${env.componentName} --from-dir=. -n ${env.projectName} --wait"
            }
         }
      }
    }
    }
    } */

    /*
    stage('Tag Image') {
            agent { 
        label 'maven'
        }
        steps {
            script {
                openshift.withCluster() {
                openshift.withProject("${env.projectName}"){
                openshift.tag("${env.componentName}:${env.latestTag}", "${env.componentName}:${env.buildTag}")
                openshift.selector("istag", "${env.componentName}:${env.latestTag}").delete()
                openshift.tag("${env.componentName}:${env.buildTag}", "${env.componentName}:${env.latestTag}")
                openshift.tag("${env.componentName}:${env.buildTag}", "${env.componentName}:${env.releaseTag}")
                openshift.tag("${env.componentName}:${env.releaseTag}", "${env.componentName}:${env.expSqdTag}", "--alias")
                }
            }
        }
    }
   }

*/
  /*
    stage('Deploy Application') {
            agent { 
        label 'maven'
        }
      steps {
        script {
            withCredentials([string(credentialsId: "${JENKINS_SA}", variable: 'TOKEN')]) {

                def check_dc = sh (
                    script: "oc --token=${TOKEN} get dc -n ${env.projectName} | grep ${env.componentName} | awk '{print \$1}'",
                    returnStdout: true
                    )
                   
                if(check_dc.contains("${env.componentName}")) {
                    echo "${check_dc} is already deployed. Performing rolling update ..."
                }
                else {
                    echo "deploying ${env.componentName} from scratch"
                    sh "oc --token=${TOKEN} new-app ${env.projectName}/${env.componentName}:latest --name ${env.componentName} -n ${env.projectName}"
                    sh "oc --token=${TOKEN} create route edge --service=${env.componentName} -n ${env.projectName}"
                }
                sleep 45
                def check_replica = sh (
                    script: "oc --token=${TOKEN} get dc ${env.componentName} -n ${env.projectName} -o jsonpath='{.spec.replicas}'",
                    returnStdout: true
                    )
                echo "{$check_replica}"    
                def available_replica = sh (
                    script: "oc --token=${TOKEN} get dc ${env.componentName} -n ${env.projectName} -o jsonpath='{.status.availableReplicas}'",
                    returnStdout: true
                    )
                echo "{$available_replica}"
                while (check_replica != available_replica) {
                    sleep 15
                    available_replica = sh (
                    script: "oc --token=${TOKEN} get dc ${env.componentName} -n ${env.projectName} -o jsonpath='{.status.availableReplicas}'",
                    returnStdout: true
                    )
                    echo "{$available_replica}"
                }
        }
        }
    }
    }
    */
    /*
    stage('Verify Deployment') {
                agent { 
        label 'maven'
        }
      steps {
        script {
          withCredentials([string(credentialsId: "${JENKINS_SA}", variable: 'TOKEN')]) {
            def check_route = sh (
                script: "oc --token=${TOKEN} get route ${env.componentName} -n ${env.projectName} -o jsonpath='{.spec.host}'",
                returnStdout: true
                )
            echo "${check_route}"

            def response = sh(script: "curl -i https://${check_route}", returnStdout: true)
            echo "${response}"
            
            if(response.contains("HTTP/1.1 200")){
            echo "Application deployed successfully"
            sh "exit 0"
            } else {
            echo "Application deployment failed"
            sh "exit 1"
            }
          }
        }
      }
    }
    */
    
/*
    stage('Test') {
                agent { 
        label 'katalon'
        }
            steps {
            script {
          withCredentials([string(credentialsId: "${JENKINS_SA}", variable: 'TOKEN')]) {
                sh 'katalon-execute.sh -browserType="Chrome" -retry=0 -statusDelay=15 -testSuitePath="Test Suites/TS_RegressionTest"'
            }
        
        
    post {
        always {
  //          archiveArtifacts artifacts: 'report', fingerprint: true
    //        junit 'report_Report.xml'
     //   }
   // }
//    }
  //  }
//    }

    
    */
    
 /*   stage ("Ignite Functional test") {		//an arbitrary stage name
        steps {
            build 'HESN-Ignite'	//this is where we specify which job to invoke.
        }
    }
   */ 

/*
    stage('Promote & Deploy Application in Prod Green Project') {
      steps {
        script {
            if(GIT_BRANCH.contains("${BR1}")){
            withCredentials([string(credentialsId: "${JENKINS_SA}", variable: 'TOKEN')]) {
                sh "oc --token=${TOKEN} adm policy add-scc-to-user anyuid system:serviceaccount:${env.projectGreen}:default"
                sh "oc --token=${TOKEN} tag ${env.projectName}/${env.componentName}:${env.buildTag} ${projectGreen}/${env.componentName}:${env.buildTag}"
                sh "oc --token=${TOKEN} tag ${env.projectGreen}/${env.componentName}:${env.buildTag} ${env.projectGreen}/${env.componentName}:latest"
                sh "oc --token=${TOKEN} policy add-role-to-user system:image-puller system:serviceaccount:${env.projectGreen}:default -n ${env.projectName}"
    
                def check_dc = sh (
                    script: "oc --token=${TOKEN} get dc -n ${env.projectGreen} | grep ${env.componentName} | awk '{print \$1}'",
                    returnStdout: true
                    )
                   
                if(check_dc.contains("${env.componentName}")) {
                    echo "${check_dc} is already deployed. Performing rolling update ..."
                    //sh "oc --token=${TOKEN} rollout latest dc/${env.componentName} -n ${env.projectGreen}"
                }
                else {
                    echo "deploying ${env.componentName} from scratch"
                    sh "oc --token=${TOKEN} new-app ${env.projectGreen}/${env.componentName}:latest --name ${env.componentName} -n ${env.projectGreen}"
                    sh "oc --token=${TOKEN} expose svc/${env.componentName} -n ${env.projectGreen}"
                
                    def backend_host = sh (
                    script: "oc --token=${TOKEN} get route ${backendApp} -n ${env.projectGreen} -o jsonpath='{.spec.host}'",
                    returnStdout: true
                    )
                    
                    echo "${backend_host}"
                    
                    sh "oc --token=${TOKEN} set env dc/${env.componentName} BACKEND_URL=https://${backend_host} -n ${env.projectGreen}"

                }
                sleep 45
                def check_replica = sh (
                    script: "oc --token=${TOKEN} get dc ${env.componentName} -n ${env.projectGreen} -o jsonpath='{.spec.replicas}'",
                    returnStdout: true
                    )
                echo "{$check_replica}"    
                def available_replica = sh (
                    script: "oc --token=${TOKEN} get dc ${env.componentName} -n ${env.projectGreen} -o jsonpath='{.status.availableReplicas}'",
                    returnStdout: true
                    )
                echo "{$available_replica}"
                while (check_replica != available_replica) {
                    sleep 15
                    available_replica = sh (
                    script: "oc --token=${TOKEN} get dc ${env.componentName} -n ${env.projectGreen} -o jsonpath='{.status.availableReplicas}'",
                    returnStdout: true
                    )
                    echo "{$available_replica}"
                }
        }
        }else{
            echo "Deployment not required for ${GIT_BRANCH} branch in this namespace"
            sh "exit 0"
        }
        }
    }
    }
    */

    /*
    stage('Verify Deployment in Prod Green Project') {
      steps {
        script {
            if(GIT_BRANCH.contains("${BR1}")){
            withCredentials([string(credentialsId: "${JENKINS_SA}", variable: 'TOKEN')]) {
            def check_route = sh (
                script: "oc --token=${TOKEN} get route ${env.componentName} -n ${env.projectGreen} -o jsonpath='{.spec.host}'",
                returnStdout: true
                )
            echo "${check_route}"

            def response = sh(script: "curl -i https://${check_route}", returnStdout: true)
            echo "${response}"
            
            if(response.contains("HTTP/1.1 200")){
            echo "Application deployed successfully"
            sh "exit 0"
            } else {
            echo "Application deployment failed"
            sh "exit 1"
            }
          }        
          }else{
            echo "Deployment not required for ${GIT_BRANCH} branch in this namespace"
            sh "exit 0"
        }
        }
      }
    }
*/
} 
}
