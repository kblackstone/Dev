
[<img src="http://azuredeploy.net/deploybutton.png"/>](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fkblackstone%2FDev%2Fmaster%2FOutbound-HA-StandardSKU-LB%2FazureDeploy.json)

As part of the deployment options:
- You MUST define a source IP address or subnet to allow management access. (0.0.0.0/0 is not allowed)

This template deploys a firewall environment that includes:

- Two Palo Alto Networks Firewalls (license type user selectable)
- One Standard SKU Internal Load Balancer (LB-Egress)
- 1 Linux Web Server
- 1 Linux Dev Server
- Multiple Subnets and UDRs to support the traffic flow

This template creates all the infrastructure and appropriate UDRs in the 10.0.0.0/16 VNET. Post-deployment tasks include:

- Configuring the FW (download and import the fw-config file that matches your licensing)
- Installation/configuration of the Apache Web Server software

To Deploy ARM Template using Azure CLI in ARM mode

- Download the two JSON files: azureDeploy.json and azureDeploy.parameters.json
- Customize the azureDeploy.parameters.json file and then deploy it from your computer.
- Install the latest Azure CLI for your computer.
- Validate and deploy the ARM template:
    azure login
    azure config mode arm
    azure  group  template  validate  -g YourResourceGroupName \
        -e  azureDeploy.json   -f  azureDeploy.parameters.json
    azure group create -v -n YourResourceGroupName -l YourAzureRegion  \
        -d  YourDeploymentLabel  -f azureDeploy.json -e azureDeploy.parameters.json

To check the status of your deployment:

- Via CLI: azure vm show -g YourResourceGroupName -n YourDeploymentLabel
- Via Azure Portal: Your Resource Group > Deployment or Alert Logs
