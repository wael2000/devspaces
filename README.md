# devspaces

Start a new workshpace 
choose the in the browser IDE (editor)
Below the supported editors 
# (1)
editor-name: Microsoft Visual Studio Code - Open Source

editor-key: che-incubator/che-code/insiders
# (2)
editor-name: JetBrains IntelliJ IDEA Community Edition

editor-key: che-incubator/che-idea/latest
# (3)
editor-name: Eclipse Theia

editor-key: eclipse/che-theia/latest

# Skopeo, copy image to Quay

# Slack integration 
Token page
https://api.slack.com/apps/A04PJBP0JBV/oauth?

https://hub.tekton.dev/tekton/task/send-to-channel-slack


# Query Quay for vulnerabilites 
https://www.redhat.com/sysadmin/using-quayio-scanner
https://quay.io/api/v1/repository/wael2000/spring-petclinic/manifest/sha256:42b0727d79e2118250eeee0c8ffc9c9c4924e4812cef59094d348c68aedf9a6c/security?vulnerabilities=true




$ IMAGE_NAME='app-sre/ubi8-ubi'
$ IMAGE_TAG='8.2-299'
$ skopeo inspect docker://quay.io/$IMAGE_NAME:$IMAGE_TAG
$ IMAGE_DIGEST=`skopeo inspect docker://quay.io/$IMAGE_NAME:$IMAGE_TAG | jq -r .Digest`
$ curl -o `basename $IMAGE_NAME`.json "https://quay.io/api/v1/repository/$IMAGE_NAME/manifest/$IMAGE_DIGEST/security?vulnerabilities=true"
$ jq '.data.Layer.Features[]' `basename $IMAGE_NAME`.json | jq -c '{"Name":.Name,"Version":.Version,"Advisory":.Vulnerabilities[]} | select(.Advisory.Severity=="High") | {"Advisory":.Advisory.Name,"Link":.Advisory.Link,"PACKAGE":.Name,"CURRENT VERSION":.Version,"FIXED IN VERSION":.Advisory.FixedBy }'


