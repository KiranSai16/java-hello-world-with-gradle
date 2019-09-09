node{
  try{
    stage('SCM Checkout'){
      git 'https://github.com/KiranSai16/java-hello-world-with-gradle.git'
     }
     
     stage('Build Automation'){
       def gradle =  tool name: 'gradle', type: 'gradle'
       sh "${gradle}/bin/gradle clean build"
     }
    
     stage('Unit Testing'){
       def gradle =  tool name: 'gradle', type: 'gradle'
       sh "${gradle}/bin/gradle clean test"
       step( [ $class: 'JacocoPublisher',execPattern: '**/build/**/**.exec'] )
     }
    
    stage('SonarQube Analysis'){
       def gradle =  tool name: 'gradle', type: 'gradle'
       withSonarQubeEnv('jenkins_sonar') {
        sh "${gradle}/bin/gradle sonarqube"
       }
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
     sh "echo "Pipeline aborted.""
     
   }
 } 

      
      
