#!/usr/bin/groovy
@Library('github.com/fabric8io/osio-pipeline@master')_

osio {

  config runtime: 'node'

  ci {

    def app = processTemplate(params: [
          RELEASE_VERSION: "1.0.${env.BUILD_NUMBER}"
    ])
    

    build resources: app, commands: """
          npm --version
          oc version
    """
    
  }
  
  

  cd {

    def resources = processTemplate(params: [
          RELEASE_VERSION: "1.0.${env.BUILD_NUMBER}"
    ])
    
    
    def route = processTemplate(file: "route.yaml")

    build resources: [resources, route], commands: """
         npm --version
         oc version
    """
    

    deploy resources: [resources, route], env: 'stage'

    deploy resources: [resources, route], env: 'run', approval: 'manual'

  }
}
