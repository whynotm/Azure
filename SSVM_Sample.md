{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "virtualMachineScaleSets_myssvmtemplatemjd_name": {
            "defaultValue": "myssvmtemplatemjd",
            "type": "String"
        },
        "virtualNetworks_vnet1_externalid": {
            "defaultValue": "/subscriptions/1efbdc08-1596-4b13-ae0a-29130c7da151/resourceGroups/create_a_load_balanced_vm_scale_set.3250222957.date.20190813192937354/providers/Microsoft.Network/virtualNetworks/vnet1",
            "type": "String"
        },
        "disks_myssvmtemplatemjd_myssvmtemplatemjd_1_OsDisk_1_8970c4c0b7474b05a9a3899502e9226a_externalid": {
            "defaultValue": "/subscriptions/1efbdc08-1596-4b13-ae0a-29130c7da151/resourceGroups/create_a_load_balanced_vm_scale_set.3250222957.date.20190813192937354/providers/Microsoft.Compute/disks/myssvmtemplatemjd_myssvmtemplatemjd_1_OsDisk_1_8970c4c0b7474b05a9a3899502e9226a",
            "type": "String"
        }
    },
    "variables": {},
    "resources": [
        {
            "type": "Microsoft.Compute/virtualMachineScaleSets",
            "apiVersion": "2019-03-01",
            "name": "[parameters('virtualMachineScaleSets_myssvmtemplatemjd_name')]",
            "location": "southcentralus",
            "sku": {
                "name": "Standard_DS1_v2",
                "tier": "Standard",
                "capacity": 1
            },
            "properties": {
                "singlePlacementGroup": true,
                "upgradePolicy": {
                    "mode": "Manual"
                },
                "virtualMachineProfile": {
                    "osProfile": {
                        "computerNamePrefix": "[concat(parameters('virtualMachineScaleSets_myssvmtemplatemjd_name'), '3')]",
                        "adminUsername": "azureuser",
                        "linuxConfiguration": {
                            "disablePasswordAuthentication": false,
                            "provisionVMAgent": true
                        },
                        "secrets": []
                    },
                    "storageProfile": {
                        "osDisk": {
                            "createOption": "FromImage",
                            "caching": "ReadWrite",
                            "managedDisk": {
                                "storageAccountType": "Premium_LRS"
                            }
                        },
                        "imageReference": {
                            "publisher": "Canonical",
                            "offer": "UbuntuServer",
                            "sku": "18.04-LTS",
                            "version": "latest"
                        }
                    },                    
					"diagnosticsProfile": { //
                        "bootDiagnostics": {
                            "enabled": true,
                            "storageUri": "https://azurelalab3r7aik4npig6u.blob.core.windows.net/"
                        }
                    },
					
					"networkProfile": {
                        "networkInterfaceConfigurations": [
                            {
                                "name": "[concat(parameters('virtualMachineScaleSets_myssvmtemplatemjd_name'), 'Nic')]",
                                "properties": {
                                    "primary": true,
                                    "enableAcceleratedNetworking": false,
                                    "dnsSettings": {
                                        "dnsServers": []
                                    },
                                    "enableIPForwarding": false,
                                    "ipConfigurations": [
                                        {
                                            "name": "[concat(parameters('virtualMachineScaleSets_myssvmtemplatemjd_name'), 'IpConfig')]",
                                            "properties": {
                                                "subnet": {
                                                    "id": "[concat(parameters('virtualNetworks_vnet1_externalid'), '/subnets/subnet1')]"
                                                },
                                                "publicIPAddressConfiguration": {
                                                    "name": "pub1",
                                                    "properties": {
                                                        "idleTimeoutInMinutes": 15,
                                                        "ipTags": []
                                                    }
                                                },
												"privateIPAddressVersion": "IPv4"
                                            }
                                        }
                                    ]
                                }
                            }
                        ]
                    },
                    "extensionProfile": {
                        "extensions": [
                            {
                                "name": "CustomScript",
                                "properties": {
                                    "autoUpgradeMinorVersion": true,
                                    "publisher": "Microsoft.Azure.Extensions",
                                    "type": "CustomScript",
                                    "typeHandlerVersion": "2.0",
                                    "settings": {
                                        "fileUris": [
                                            "https://iaasv2tempstorageam.blob.core.windows.net/vmextensionstemporary-10032000595838e6-20190813193742155/script.sh?sv=2017-04-17&sr=c&sig=Ds3FFxpK7yrFyoeM9dN%2FPktSVPXBW%2B7JmRuxplGDdyQ%3D&se=2019-08-14T19%3A37%3A42Z&sp=rw"
                                        ]
                                    }
                                }
                            }
                        ]
                    },
                    "priority": "Regular"
                },
                "overprovision": true,
                "doNotRunExtensionsOnOverprovisionedVMs": false,
                "platformFaultDomainCount": 5
            }
        },
        {
            "type": "Microsoft.Compute/virtualMachineScaleSets/extensions",
            "apiVersion": "2019-03-01",
            "name": "[concat(parameters('virtualMachineScaleSets_myssvmtemplatemjd_name'), '/CustomScript')]",
            "dependsOn": [
                "[resourceId('Microsoft.Compute/virtualMachineScaleSets', parameters('virtualMachineScaleSets_myssvmtemplatemjd_name'))]"
            ],
            "properties": {
                "provisioningState": "Succeeded",
                "autoUpgradeMinorVersion": true,
                "publisher": "Microsoft.Azure.Extensions",
                "type": "CustomScript",
                "typeHandlerVersion": "2.0",
                "settings": {
                    "fileUris": [
                        "https://iaasv2tempstorageam.blob.core.windows.net/vmextensionstemporary-10032000595838e6-20190813193742155/script.sh?sv=2017-04-17&sr=c&sig=Ds3FFxpK7yrFyoeM9dN%2FPktSVPXBW%2B7JmRuxplGDdyQ%3D&se=2019-08-14T19%3A37%3A42Z&sp=rw"
                    ]
                }
            }
        },
        {
            "type": "Microsoft.Compute/virtualMachineScaleSets/virtualMachines",
            "apiVersion": "2019-03-01",
            "name": "[concat(parameters('virtualMachineScaleSets_myssvmtemplatemjd_name'), '/1')]",
            "location": "southcentralus",
            "dependsOn": [
                "[resourceId('Microsoft.Compute/virtualMachineScaleSets', parameters('virtualMachineScaleSets_myssvmtemplatemjd_name'))]"
            ],
            "sku": {
                "name": "Standard_DS1_v2",
                "tier": "Standard"
            },
            "properties": {
                "networkProfileConfiguration": {
                    "networkInterfaceConfigurations": [
                        {
                            "name": "myssvmtemplatemjdNic",
                            "properties": {
                                "primary": true,
                                "enableAcceleratedNetworking": false,
                                "dnsSettings": {
                                    "dnsServers": []
                                },
                                "enableIPForwarding": false,
                                "ipConfigurations": [
                                    {
                                        "name": "myssvmtemplatemjdIpConfig",
                                        "properties": {
                                            "subnet": {
                                                "id": "[concat(parameters('virtualNetworks_vnet1_externalid'), '/subnets/subnet1')]"
                                            },
                                            "privateIPAddressVersion": "IPv4"
                                        }
                                    }
                                ]
                            }
                        }
                    ]
                },
                "hardwareProfile": {},
                "storageProfile": {
                    "imageReference": {
                        "publisher": "Canonical",
                        "offer": "UbuntuServer",
                        "sku": "18.04-LTS",
                        "version": "18.04.201907221"
                    },
                    "osDisk": {
                        "osType": "Linux",
                        "name": "myssvmtemplatemjd_myssvmtemplatemjd_1_OsDisk_1_8970c4c0b7474b05a9a3899502e9226a",
                        "createOption": "FromImage",
                        "caching": "ReadWrite",
                        "managedDisk": {
                            "storageAccountType": "Premium_LRS",
                            "id": "[parameters('disks_myssvmtemplatemjd_myssvmtemplatemjd_1_OsDisk_1_8970c4c0b7474b05a9a3899502e9226a_externalid')]"
                        },
                        "diskSizeGB": 30
                    },
                    "dataDisks": []
                },
                "osProfile": {
                    "computerName": "myssvmtemplatemjd3000001",
                    "adminUsername": "azureuser",
                    "linuxConfiguration": {
                        "disablePasswordAuthentication": false,
                        "provisionVMAgent": true
                    },
                    "secrets": [],
                    "allowExtensionOperations": true
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[concat(resourceId('Microsoft.Compute/virtualMachineScaleSets/virtualMachines', parameters('virtualMachineScaleSets_myssvmtemplatemjd_name'), '1'), '/networkInterfaces/myssvmtemplatemjdNic')]"
                        }
                    ]
                }
            }
        }
    ]
}