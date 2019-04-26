node('linux'){
    stage('UnitTest'){
        git 'https://github.com/lshen-Lorraine/java-project.git'
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
    }
    
    stage('Build'){
        sh 'ant -f build.xml -v'
    }
    stage('Deploy'){
        sh "aws s3 cp $WORKSPACE/java-pipeline/dist/*.jar  s3://seis6651/rectangle-${BUILD_NUMBER}.jar"
    }
    stage('Report'){
      
        sh 'aws cloudformation describestack-resources --region us-east-1 --stack-name jenkins'
        

         
    }
}
