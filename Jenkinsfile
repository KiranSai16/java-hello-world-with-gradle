def props;

node{
  try{
    stage('SCM Checkout'){
      props = readProperties  file: """pipeline.properties"""
      git branch: ${props['branch']}, url: ${props['github_url']}
    }
     
     stage('Build Automation'){
       def gradle =  tool name: 'gradle', type: 'gradle'
       sh "${gradle}/bin/gradle clean build"
       step( [ $class: 'JacocoPublisher',execPattern: '**/build/**/**.exec'] )
    }
    
    stage('SonarQube Analysis'){
       //def gradle =  tool name: 'gradle', type: 'gradle'
       //withSonarQubeEnv('jenkins_sonar') {
        //sh "${gradle}/bin/gradle sonarqube"
       //}
       def Sonarscanner = tool 'Sonarscanner';
       sh "${Sonarscanner}/sonar-scanner"
    }
    
    stage("QUALITY GATE"){  
       timeout(time: 1, unit: 'HOURS') {
         def qg = waitForQualityGate()  
         if (qg.status != 'OK') {  
           error "Pipeline aborted due to quality gate failure: ${qg.status}"  
         }
       }
     }
   }
   catch (err){
     sh "echo 'Pipeline aborted.'"
     
   }
 } 

      
      
