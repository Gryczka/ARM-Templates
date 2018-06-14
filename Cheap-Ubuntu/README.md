# Cheap-Ubuntu
This ARM template allows you to deploy the (as of Mid 2018) cheapest VM option with Ubuntu installed.

Default Ubuntu version in this template is 16.04 LTS, but options for 14.04 LTS and 17.10 are also present.
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FGryczka%2FARM-Templates%2Fmaster%2FCheap-Ubuntu%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

## Limitations
* __Password Authentication is Disabled__
    * You need to provide an ssh public key
        * You can generate one by running `ssh-keygen -t rsa -b 2048` in a linux terminal, or using putty on windows
* __Only SSH is Allowed for Inbound Ports__
    * This can be solved by changing the `securityRules` on line 193
* __Diagnostics Storage Account Name is tied to the Resource Group Name__
    * Limits this template to deploying 1 vm per rg
    * RGs with names that are only differentiated by the characters _[ '.', '-', '_', '(', ')']_ will have Diagnostic Storage Account name overlap and cause failure for the second run of the template
        * e.g. `ResourceGroupName` and `Resource.Group-Name`
            * First run with `ResourceGroupName` will succeed, second run with `Resource.Group-Name` will fail
    * This behaviour can be changed by altering the `diagnosticStorageAccountName` on line 47