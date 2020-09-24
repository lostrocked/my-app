node {
//   Accessing data from currentBuild objects

  echo "Current Build Absolute URL ${currentBuild.absoluteUrl}"
  echo "Current Build Result ${currentBuild.currentResult}"
  
//   Accessing data from env object

  echo "Jenkins Home ${env.JENKINS_HOME}"
  echo "Jenkins URL ${env.JENKINS_URL}"
  echo "JOB Name ${env.JOB_NAME}"
  
}
properties([pipelineTriggers([pollSCM('')])])
node{
   jdk = tool name: 'JDK18-211'
   env.JAVA_HOME = "${jdk}"
   stage('SCM Checkout'){
     git url:'https://github.com/lostrocked/my-app', branch: 'master'
   }
   stage('Compile-Package'){
      // Get maven home pathJDK18-211
      def mvnHome =  tool name: 'apache-maven-3.6.1', type: 'maven'   
      sh "${mvnHome}/bin/mvn package"
   }
   
   stage('Deploy'){

       echo "Jenkins Home ${env.JENKINS_HOME}"
       echo "Jenkins URL ${env.JENKINS_URL}"
       echo "JOB Name ${env.JOB_NAME}"
       runRADeployment addPackage: false, application: 'myweb', artifactVersions: [[artifactDef: '', 
       artifactType: '', artifactVersion: "1Version-${env.BUILD_ID}", artifactVersionDesc: '', 
       artifactsSource: [httpFilePath: '', httpPassword: '', httpUrl: '', httpUserName: '', 
       sourceType: 'HTTP', svnAllowUnrevisioned: false], retrievalAgents: [agentName: '', retrieveBy: 'Agents'], 
       storeInRepository: false, validateMD5: false]], build: "BBH-Unit-ID-${env.BUILD_ID}", 
       deploymentDesc: "BBH-Unit-Deploy-${env.BUILD_ID}", deploymentName: "BBH-Unit-Deploy-${env.BUILD_ID}", 
       deploymentPlanDesc: "BBH-Unit-${env.BUILD_ID}", deploymentPlanName: "BBH-Unit-${env.BUILD_ID}", 
       deploymentPlanUsage: 'Create new deployment plan everytime', deploymentProjectName: 'SomeApplication-Deploy-1', 
       deploymentStageToRun: 'Full', environments: 'Unit', failBuild: false, failedPaused: true, 
       hostName: 'lvndev002945.bpc.broadcom.net', manifestXMLGenerate: true, manifestXMLUpload: false, 
       packageDesc: '', packageName: '', packageXMLGenerate: false, packageXMLUpload: false, 
       port: '9080', pw: 'suser', runAsync: false, showDebug: false, stepParameters: [[parameterName: '', 
       parameterTypes: [parameterType: 'ApplicationType'], parameterValues: [strValue: '', 
       templatePropertyPass: false, templatePropertyStr: false, valueType: 'String'], processName: '', 
       stageName: 'Initialization', stepName: '']], templateCategoryName: 'SomeApplication1-Temp1', 
       templateName: 'Deployment-Tomcat', templateProperties: [[propertyName: 'workspace', 
       propertyValue: '/opt/my-app']], timeout: '-1', updateManifest: true, updateStepParameters: false, 
       updateTemplateProperties: true, uploadManifestXML: '', uploadPackageXML: '', 
       useCentlCrd: false, useSSL: false, user: 'superuser'
   }
}
