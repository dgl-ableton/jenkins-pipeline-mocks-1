@Library([
  'ableton-utils@0.10',
  'groovylint@0.4',
]) _


runTheBuilds.runDevToolsProject(
  test: {
    parallel(failFast: false,
      groovylint: {
        groovylint.check('./Jenkinsfile,./*.gradle,**/*.groovy')
      },
      junit: {
        try {
          sh './gradlew test'
        } finally {
          junit 'build/test-results/**/*.xml'
        }
      },
    )
  },
  deploy: {
    runTheBuilds.withBranches(branches: ['master'], acceptPullRequests: false) {
      String versionNumber = readFile('VERSION').trim()
      version.tag(versionNumber)
      version.forwardMinorBranch(versionNumber)
    }
  },
)
