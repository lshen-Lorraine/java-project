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
        sh "aws s3 cp $WORKSPACE/dist/*.jar  s3://seis6651/rectangle-${BUILD_NUMBER}.jar"
    }
    stage('Report'){
        
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '921dec39-104b-4ce9-9998-e0b52249ce4d', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
           sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
        }

         
    }
}
