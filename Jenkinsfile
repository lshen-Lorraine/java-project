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
        sh "aws s3 cp *.jar test.txt s3://seis6651/rectangle-${BUILD_NUMBER}.jar"
    }
    stage('Report'){
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AKIA3YE5K52FU4GSQFHD', credentialsId: '921dec39-104b-4ce9-9998-e0b52249ce4d', secretKeyVariable: '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']]) {
    // some block
            sh 'aws cloudformation describestack-resources --region us-east-1 --stack-name jenkins'
        }

         
    }
}
