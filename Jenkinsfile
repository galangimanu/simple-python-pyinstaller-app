node {
    // This step should not normally be used in your script. Consult the inline help for details.
    withDockerContainer('python:2-alpine') {
        // some block
        stage('Build') {
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
        }
    }
    withDockerContainer('qnib/pytest') {
        // some block
        stage('Test') {
            sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            junit 'test-reports/results.xml'
        }
    }
    withDockerContainer('cdrx/pyinstaller-linux:python2') {
        // some block
        stage('Deliver') {
            sh 'pyinstaller --onefile sources/add2vals.py'
            archiveArtifacts artifacts: 'dist/add2vals', followSymlinks: false
        }
    }
}