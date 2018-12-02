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
        echo ${BUILD_NUMBER}
        echo '/workspace/java-pipeline/dist/rectangle-${BUILD_NUMBER}.jar'
        aws s3 cp '/workspace/java-pipeline/dist/rectangle-${BUILD_NUMBER}.jar' 's3://seis665-assignment10-java-project'
    }
}
