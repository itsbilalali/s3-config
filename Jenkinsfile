pipeline {
    agent any

    environment {
        CONFIG_FILE = 'config.json'
    }

    stages {
        stage('Sync Active to Failover') {
            steps {
                script {
                    // Load the configuration file
                    def config = readJSON file: "${CONFIG_FILE}"
                    
                    // Iterate over the buckets and sync active to failover
                    config.s3.each { bucket ->
                        def activeBucket = bucket.active
                        def failoverBucket = bucket.failover
                        
                        echo "Syncing Active Bucket: ${activeBucket} to Failover Bucket: ${failoverBucket}"
                        // Run AWS CLI command to sync active to failover
                        sh "aws s3 sync s3://${activeBucket} s3://${failoverBucket}"
                    }
                }
            }
        }
    }
    

}
