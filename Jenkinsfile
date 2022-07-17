pipeline {
  agent any
  parameters {
    string(name: 'OPENCUE_RELEASE_VERSION', defaultValue: '0.15.22', description: 'Opencue Version')
    string(name: 'PYTHON_EXEC', defaultValue: '/codecg/tools/bin/python3', description: 'Python Executable to use')
    string(name: 'INSTALL_PREFIX', defaultValue: '/codecg/tools/opencue', description: 'Path to install')
  }
  stages {
    stage('Download') {
      when {
        branch 'main'
      }
      steps {
        sh 'rm -f *.gz'
        sh 'wget https://github.com/AcademySoftwareFoundation/OpenCue/releases/download/v${OPENCUE_RELEASE_VERSION}/pycue-${OPENCUE_RELEASE_VERSION}-all.tar.gz'
        sh 'wget https://github.com/AcademySoftwareFoundation/OpenCue/releases/download/v${OPENCUE_RELEASE_VERSION}/pyoutline-${OPENCUE_RELEASE_VERSION}-all.tar.gz'
        sh 'wget https://github.com/AcademySoftwareFoundation/OpenCue/releases/download/v${OPENCUE_RELEASE_VERSION}/cuesubmit-${OPENCUE_RELEASE_VERSION}-all.tar.gz'
        sh 'wget https://github.com/AcademySoftwareFoundation/OpenCue/releases/download/v${OPENCUE_RELEASE_VERSION}/cuegui-${OPENCUE_RELEASE_VERSION}-all.tar.gz'
        sh 'wget https://github.com/AcademySoftwareFoundation/OpenCue/releases/download/v${OPENCUE_RELEASE_VERSION}/cueadmin-${OPENCUE_RELEASE_VERSION}-all.tar.gz'
        sh 'tar xfv cueadmin-${OPENCUE_RELEASE_VERSION}-all.tar.gz'
        sh 'tar xfv cuesubmit-${OPENCUE_RELEASE_VERSION}-all.tar.gz'
        sh 'tar xfv pyoutline-${OPENCUE_RELEASE_VERSION}-all.tar.gz'
        sh 'tar xfv cuegui-${OPENCUE_RELEASE_VERSION}-all.tar.gz'
        sh 'tar xfv pycue-${OPENCUE_RELEASE_VERSION}-all.tar.gz'
      }
    }
    stage('Install') {
      when {
        branch 'main'
      }
      steps {
        sh '${PYTHON_EXEC} -m venv ${INSTALL_PREFIX}'
        sh 'cd pycue-${OPENCUE_RELEASE_VERSION}-all && source ${INSTALL_PREFIX}/bin/activate && python -m pip install -r requirements.txt && python setup.py install'
        sh 'cd pyoutline-${OPENCUE_RELEASE_VERSION}-all && source ${INSTALL_PREFIX}/bin/activate && python -m pip install -r requirements.txt && python setup.py install'
        sh 'cd cueadmin-${OPENCUE_RELEASE_VERSION}-all && source ${INSTALL_PREFIX}/bin/activate && python -m pip install -r requirements.txt && python setup.py install'
        sh 'cd cuegui-${OPENCUE_RELEASE_VERSION}-all && source ${INSTALL_PREFIX}/bin/activate && python -m pip install -r requirements.txt && python setup.py install'
        sh 'cd cuesubmit-${OPENCUE_RELEASE_VERSION}-all && source ${INSTALL_PREFIX}/bin/activate && python -m pip install -r requirements.txt && python setup.py install'
        sh 'cd cuesubmit-${OPENCUE_RELEASE_VERSION}-all && cp -r plugins ${INSTALL_PREFIX}'
      }
    }
  }
}
