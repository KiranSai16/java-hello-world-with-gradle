node{
  try{
    stage('SCM Checkout'){
      git 'https://github.com/KiranSai16/java-hello-world-with-gradle.git'
     }
     
     stage('Build Automation'){
       def gradle =  tool name: 'gradle', type: 'gradle'
       sh "${gradle}/bin/gradle clean build"
       step( [ $class: 'JacocoPublisher',execPattern: '**/build/**/**.exec'] )
     }
    
     stage('Unit Testing'){
       def gradle =  tool name: 'gradle', type: 'gradle'
       sh "${gradle}/bin/gradle test jacoco"
     }
    }
  catch (err){
   }
  } 
      
      
