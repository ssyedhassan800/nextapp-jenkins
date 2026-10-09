node {
    def appDir = '/var/www/nextjs-app'

    stage('clean workspace'){
        echo 'cleaning workspace'
        deleteDir()
    }

    stage('clone repo'){
        echo 'cloning repo'
        git (
            branch: 'main',
            url: 'https://github.com/ssyedhassan800/nextapp-jenkins'        )
    }

    stage('Deploy in ec2'){
        echo 'Deploying in ec2'
        sh """
            sudo mkdir -p ${appDir}
            sudo chown -R jenkins:jenkins ${appDir}
            rsync -av --exclude='.git' --exclude='node_modules' ./ ${appDir}
            
            cd ${appDir}
            sudo npm install
            sudo npm run build
            sudo fuser -k 3000/tcp || true
            npm run start
        """
    }
}