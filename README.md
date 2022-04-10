# KPMG_Challenge

Challenge#1

**Solution:**

I have chosen Azure for designing a 3-tier architecture. I have designed a basic setup using only IAAS.

3 layers created

1. Web Layer for Public facing
2. Application layer have the business logic
3. DB layer for storing the data.

Resources used:

VM - Availability set
Vent
Subnets
Publicip
Application Load Balancer for external traffic.
Standard load balancer for routing between App and DB layer internal traffic.
Network security groups for restricting the traffic using inbound/outbound rules.

Created a design in Draw.io and saged as png by name - 3-Tier_Architecture.drawio.PNG


The solution can be more enhanced based upon the type of requirement, but i have just done a basic setup using IAAS services alone, We can utilize the wide range of PAAS services as well depends on a business requirements.

Challenge#2

**Solution**

Retreiving the metadata of an instance can be done using API calls that eventually returns the response in Json format.

For Azure:

IMDS is a REST API that's available at a well-known, non-routable IP address (169.254.169.254). You can only access it from within the VM. Communication between the VM and IMDS never leaves the host. Have your HTTP clients bypass web proxies within the VM when querying IMDS, and treat 169.254.169.254 the same as 168.63.129.16.

Powershell command for invoking an API : 
Invoke-RestMethod -Headers @{"Metadata"="true"} -Method GET -NoProxy -Uri "http://169.254.169.254/metadata/instance?api-version=2021-02-01" | ConvertTo-Json -Depth 64

Ex Json Response:

{
    "compute": {
        "azEnvironment": "AZUREPUBLICCLOUD",
        "extendedLocation": {
            "type": "edgeZone",
            "name": "microsoftlosangeles"
        },
        "evictionPolicy": "",
        "isHostCompatibilityLayerVm": "true",
        "licenseType":  "Windows_Client",
        "location": "westus",
        "name": "examplevmname",
        "offer": "WindowsServer",
        "osProfile": {
            "adminUsername": "admin",
            "computerName": "examplevmname",
            "disablePasswordAuthentication": "true"
        },
        "osType": "Windows",
        "placementGroupId": "f67c14ab-e92c-408c-ae2d-da15866ec79a",
        "plan": {
            "name": "planName",
            "product": "planProduct",
            "publisher": "planPublisher"
        },
        "platformFaultDomain": "36",
        "platformSubFaultDomain": "",        
        "platformUpdateDomain": "42",
        "priority": "Regular",
        "publicKeys": [{
                "keyData": "ssh-rsa 0",
                "path": "/home/user/.ssh/authorized_keys0"
            },
            {
                "keyData": "ssh-rsa 1",
                "path": "/home/user/.ssh/authorized_keys1"
            }
        ],
        "publisher": "RDFE-Test-Microsoft-Windows-Server-Group",
        "resourceGroupName": "macikgo-test-may-23",
        "resourceId": "/subscriptions/xxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx/resourceGroups/macikgo-test-may-23/providers/Microsoft.Compute/virtualMachines/examplevmname",
        "securityProfile": {
            "secureBootEnabled": "true",
            "virtualTpmEnabled": "false"
        },
        "sku": "2019-Datacenter",
        "storageProfile": {
            "dataDisks": [{
                "bytesPerSecondThrottle": "979202048",
                "caching": "None",
                "createOption": "Empty",
                "diskCapacityBytes": "274877906944",
                "diskSizeGB": "1024",
                "image": {
                  "uri": ""
                },
                "isSharedDisk": "false",
                "isUltraDisk": "true",
                "lun": "0",
                "managedDisk": {
                  "id": "/subscriptions/xxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx/resourceGroups/macikgo-test-may-23/providers/Microsoft.Compute/disks/exampledatadiskname",
                  "storageAccountType": "StandardSSD_LRS"
                },
                "name": "exampledatadiskname",
                "opsPerSecondThrottle": "65280",
                "vhd": {
                  "uri": ""
                },
                "writeAcceleratorEnabled": "false"
            }],
            "imageReference": {
                "id": "",
                "offer": "WindowsServer",
                "publisher": "MicrosoftWindowsServer",
                "sku": "2019-Datacenter",
                "version": "latest"
            },
            "osDisk": {
                "caching": "ReadWrite",
                "createOption": "FromImage",
                "diskSizeGB": "30",
                "diffDiskSettings": {
                    "option": "Local"
                },
                "encryptionSettings": {
                    "enabled": "false"
                },
                "image": {
                    "uri": ""
                },
                "managedDisk": {
                    "id": "/subscriptions/xxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx/resourceGroups/macikgo-test-may-23/providers/Microsoft.Compute/disks/exampleosdiskname",
                    "storageAccountType": "StandardSSD_LRS"
                },
                "name": "exampleosdiskname",
                "osType": "Windows",
                "vhd": {
                    "uri": ""
                },
                "writeAcceleratorEnabled": "false"
            },
            "resourceDisk": {
                "size": "4096"
            }
        },
        "subscriptionId": "xxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",
        "tags": "baz:bash;foo:bar",
        "userData": "Zm9vYmFy",
        "version": "15.05.22",
        "virtualMachineScaleSet": {
            "id": "/subscriptions/xxxxxxxx-xxxxx-xxx-xxx-xxxx/resourceGroups/resource-group-name/providers/Microsoft.Compute/virtualMachineScaleSets/virtual-machine-scale-set-name"
        },
        "vmId": "02aab8a4-74ef-476e-8182-f6d2ba4166a6",
        "vmScaleSetName": "crpteste9vflji9",
        "vmSize": "Standard_A3",
        "zone": ""
    },
    "network": {
        "interface": [{
            "ipv4": {
               "ipAddress": [{
                    "privateIpAddress": "10.144.133.132",
                    "publicIpAddress": ""
                }],
                "subnet": [{
                    "address": "10.144.133.128",
                    "prefix": "26"
                }]
            },
            "ipv6": {
                "ipAddress": [
                 ]
            },
            "macAddress": "0011AAFFBB22"
        }]
    }
}

You can use json query language to retrieve the particualr data key.

Ex: If i want to retrieve the OS type from above Josn the use below Json Query

$.compute.osType - This will retrieve only "Windows" from above Json.

Some endpoints may return larger Json blobs in this case we can use appending route parameters to the request endpoint to filter down to a subset of the response.


Challenge#3

**Solution**

I chosed Python as a programming language to implement this logic.
Here is the code snippet for the same.

Synopsis:
Import Json - Is built-in package which can be used to work with JSON data.
used json.loads method for parsing the json
used key.splits for to split that dictionary into keys and values into different lists.
Used the for loop for iterating the dictionary to locate the value


***********************CODE************************


import json


obj = input('Enter the object - ')
key = input('Enter the Key -')
input = json.loads(obj)

def function(input,key):
  list = key.split('/')
  for i in list:
    input = input[i]
   
  return input

value =  function(input,key)
print('Value is - ' + value)

***********************************************************

PFA attached executed code snippet to get the vaue 'a'

File name: Python-Script_To resolve the Nested Object.png



