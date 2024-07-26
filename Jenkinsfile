pipeline {
    agent any

    parameters {
        string(name: 'JMeterPath', defaultValue: 'C:\\apache-jmeter-5.6.3\\bin', description: 'JMeter path')
        string(name: 'JMeterFile', defaultValue: 'Products.jmx', description: 'JMeter test plan file')
        string(name: 'THREADS', defaultValue: '5', description: 'Number of threads')
        string(name: 'RAMP_UP', defaultValue: '10', description: 'Ramp-up period')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', 
                url: 'https://github.com/hersannfonseca/qa-performance-testing.git'
            }
        }
        stage('Run test') {
            steps {
                bat 'cd ${params.JMeterPath} && jmeter -n -t ${params.JMeterFile} -l results.jtl -Jthreads=${params.THREADS} -Jramp_up=${params.RAMP_UP}'
            }
        }
        stage('Publish Report') {
            steps {
                publishPerformanceTestReport(target: [
                    reportFile: 'results.jtl',
                    format: 'JMeter'
                ])
            }
        }
    }
}