node('linux') {
    stage('Unit Tests') {
        git 'https://github.com/CHRI4177/java-project.git'
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'       
    }
    stage('Build') {
        sh 'ant -f build.xml -v'
    }
    stage('Deploy') {
        sh "aws s3 cp /workspace/java-pipeline/dist/rectangle-${env.BUILD_NUMBER}.jar s3://seis665-assignment10-java-project"
    }
    stage('Report'){
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '3566701e-df1a-4aae-a13d-c917d0b9de36', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
        }
    }
}
