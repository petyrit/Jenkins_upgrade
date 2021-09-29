//def jobs = ["JobA","JobB","JobC"]
def jobs = Eval.me(listche)
//def jobs = params.listche
//def jobs = new File("${workspace}/apps.txt").text.readLines()

def parallelStagesMap = jobs.collectEntries {
    ["${it}" : generateStage(it)]
}
 
def generateStage(job) {
    return {
        stage("stage: ${job}") {
                echo "This is ${job}."
                echo "This is ${listche}"
        }
    }
}
 
pipeline {
    agent none
 
    stages {
        stage('non-parallel stage') {
            steps {
                echo 'This stage will be executed first.'
            }
        }
 
        stage('parallel stage') {
            steps {
                script {
                    parallel parallelStagesMap
                }
            }
        }
    }
}
