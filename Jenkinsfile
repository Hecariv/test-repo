@Library('Codebeamer-CI@ALM-12241') _

node{

    Map scmVars
        stage('checkout') {
                    scmVars = checkout([
                                $class                           : 'GitSCM',
                                branches                         : scm.branches,
                                doGenerateSubmoduleConfigurations: scm.doGenerateSubmoduleConfigurations,
                                extensions                       : [
                                        [$class     : 'LocalBranch',
                                            localBranch: '' // the branch name is computed from the remote branch without the origin
                                        ],
                                        [
                                                $class: 'WipeWorkspace'
                                        ]
                                ],
                                userRemoteConfigs                : scm.userRemoteConfigs
                        ])

                        // include commit in BuildRun description
                        currentBuild.description = "${scmVars.GIT_COMMIT}"

            }


    stage('Configuration') {
            sh "echo 'HELLO WORLD!!!'"
            sh "echo 'Configuration'"
            configureProject();
        }

}
