node {
   def commit_id
   stage('Preparation') {
     checkout scm
     sh "git rev-parse --short HEAD > .git/commit-id"                        
     commit_id = readFile('.git/commit-id').trim()
   }
   stage('test') {
     nodejs(nodeJSInstallationName: 'nodejs') {
       sh 'npm install --only=dev'
       sh 'npm test'
     }
   }
   stage('docker build/push') {
     docker.withRegistry('https://index.docker.io/v2/', '8b182da1-7838-4cd7-ac34-f9ff2c0b2075') {
       def app = docker.build("marvelino12/docker-node-demo-ba:${commit_id}", '.').push()
     }
   }
}
