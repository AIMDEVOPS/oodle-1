env.dockerimagename="buildon/buildon:v2"
//def jupiter_host='34.200.55.25'
def jupiter_jost='awseb-e-a-awsebloa-1kk591tzzgqvb-372758977.us-east-1.elb.amazonaws.com'
def talend_cmd_host='34.237.156.239'
def talend_cmd_user='admin@company.com'
node {
    stage ('Code Checkout') {
        checkout scm
        echo "Listing the files in the current dir"
        sh """ls -ltr
       pwd
       """

    }
    stage ('Code compile') {
        sh """pwd
          cd "${WORKSPACE}/OODLE"
          mvn org.talend:ci.builder:6.3.1:generate -f pom.xml -Dcommandline.workspace="${WORKSPACE}/OODLE/process/" -Dcommandline.host=${talend_cmd_host} -Dcommandline.port=8002 -Dcommandline.user=${talend_cmd_user}
          ls -ltr
          """
        sh 'sleep 10s'
    }
    stage ('Code Build') {
        sh """pwd
          ls -ltr
          cd "${WORKSPACE}/OODLE"
          mvn package -f pom.xml -Dcommandline.workspace="${WORKSPACE}/OODLE/process/" -Dcommandline.host=${talend_cmd_host} -Dcommandline.port=8002 -Dcommandline.user=${talend_cmd_user} -DprojectsTargetDirectory="${WORKSPACE}/OODLE/target"
          """
        sh 'sleep 10s'
    }
    stage ('Code Deploy') {
        echo "Deploying code"
        sh"""
      cd "${WORKSPACE}/OODLE/"
      ls -ltr
      pwd
      set +e
      mvn deploy -fn -e -s settings.xml
      set +e
    """
    }
    stage ('Executing the tests') {
        echo "Executing the tests"
        sh"""
            echo "Deployed and Tested"
        """
    }
}
