# cloud-pak-deployer-gitops

This repo is using [Cloud pak deployer](https://ibm.github.io/cloud-pak-deployer).

This repo has two purposes:
1. Build the Cloud pak deployed in Openshift making it available to deploying Cloud paks.
2. Containing the configuration that will be used by the Cloud pak deployer

## Instructions

1. Fork this repo if you want to change the configuration in /config. Make sure to update the [URL to the git repo](https://github.com/thomas-mattsson/cloud-pak-deployer-gitops/blob/main/resources/resources.yaml#L7) if doing so.
2. If forked, update the configuration files in /config to match the wanted environment. See details in the cloud pak deployer instuctions. ocp.yaml will be automatically updated with the base domain and cluster name.
3. Run the following commands to build cloud pak deployer
```bash
oc create -f https://raw.githubusercontent.com/thomas-mattsson/cloud-pak-deployer-gitops/main/resources/build.yaml
```
4. Wait until the build above is finished. You can track it in the Builds/Builds section in the Openshift console.
5. Run the following commands. You will need to insert your IBM entitlement registry key where indicated. 
```bash
oc create secret generic cloud-pak-deployer-input -n cloud-pak-deployer --from-literal entitlement-key="<your entitlement key>"
oc create -f https://raw.githubusercontent.com/thomas-mattsson/cloud-pak-deployer-gitops/main/resources/resources.yaml
```
