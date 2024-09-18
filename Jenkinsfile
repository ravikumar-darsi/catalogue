#!groovy
@Library('roboshop-shared-library') _

// responsibility to pass what type of application and component is this to pipeline deicssion

def configMap = [  // def is used to create a variable in groovy script
    application: "nodejsVM",
    component: "catalogue"
]
if( ! env.BRANCH_NAME.equalsIgnoreCase('main')){
    pipelineDecission.decidePipeline(configMap)
}
else{
    echo "This is PRODUCTION, deal with CR process"
}