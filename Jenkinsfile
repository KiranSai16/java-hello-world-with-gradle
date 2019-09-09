node{
  try{
    stage('SCM Checkout'){
      git 'https://github.com/KiranSai16/java-hello-world-with-gradle.git'
     }
     
     stage('Build Automation'){
       def gradle =  tool name: 'gradle', type: 'gradle'
       sh "${gradle} build "
     }
    }
  catch (err){
   }
  } 
      
      
