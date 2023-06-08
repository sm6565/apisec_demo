pipeline {
    agent any

    stages {
        
        stage('scan') {
            steps { withCredentials([string(credentialsId: 'PCC_CONSOLE_URL', variable: 'CONSOLE'), string(credentialsId: 'PCC_PASS', variable: 'PASS'), string(credentialsId: 'PCC_USER', variable: 'USER')]) {
   
      sh '''
            echo "$CONSOLE"
            curl -k -u "$USER":"$PASS" $CONSOLE/api/v1/util/twistcli --output ./twistcli 
            chmod a+x ./twistcli
            ./twistcli waas openapi-scan  --address "$CONSOLE" --user "$USER"  --password "$PASS" uber.yaml
            '''
      }
            }
        }
        stage('Cleanup') {
            steps {
                echo 'Cleaning..'
                echo 'Running docker rmi..'
            }
        }
    }
}
//