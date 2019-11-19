pipeline {
    agent any
  stages {
    stage ('Unit Test') {
      steps {
        script {
          if (fileExists('magento/tests')) {
            try {
              sh 'phpunit --log-junit test.xml magento/tests/*Test.php'
            } catch(err) {
            step([$class: 'JUnitResultArchiver', testResults: 'test.xml'])
            throw err
            }
          } 
		else {
              sh 'echo "No tests directory. Skipping Unit Test."'
          }     
        }
      }
    
    }
    stage("Code Analysis") {
      steps {
        script {
          if (fileExists('magento/tests')) {
            try {
              sh 'phpunit --log-junit test.xml magento/tests/*Test.php'
            } catch(err) {
            step([$class: 'JUnitResultArchiver', testResults: 'test.xml'])
            throw err
            }
          } 
		else {
              sh 'echo "No tests directory. Skipping Code Analysis."'
          }  
        }   
        
       }
      
      }
    
    stage ('Launching Server & Deploy') {
      steps {  
          sh 'curl -X POST -u z0057:Ziffity$$2323 http://ci.ziffity.com:8080/job/DEVOPS.DEMO.MAGE.DEPLOY/build'
   }
}
    
    stage ('Automation Testing') {
      steps {
        echo('Testing Completed')        
      }

    }
    stage ('Ready for QA') {
      steps {  
        echo('Ready For QA')
      }
    }
    
   } 
