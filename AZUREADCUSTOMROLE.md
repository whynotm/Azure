# Basic role information
$displayName = "Custom Application Support Administrator"
$description = "Can manage basic aspects of application registrations."
$templateId = (New-Guid).Guid


# Set of permissions to grant
$allowedResourceAction =
@(
"microsoft.directory/applications/create",
"microsoft.directory/applications/delete",
"microsoft.directory/applications/applicationProxy/read",
"microsoft.directory/applications/applicationProxy/update",
"microsoft.directory/applications/applicationProxyAuthentication/update",
"microsoft.directory/applications/applicationProxySslCertificate/update",
"microsoft.directory/applications/applicationProxyUrlSettings/update",
"microsoft.directory/applications/audience/update",
"microsoft.directory/applications/authentication/update",
"microsoft.directory/applications/basic/update",
"microsoft.directory/applications/credentials/update",
"microsoft.directory/applications/owners/update",
"microsoft.directory/applications/permissions/update",
"microsoft.directory/applicationTemplates/instantiate",
"microsoft.directory/auditLogs/allProperties/read",
"microsoft.directory/applicationPolicies/create",
"microsoft.directory/applicationPolicies/delete",
"microsoft.directory/applicationPolicies/standard/read",
"microsoft.directory/applicationPolicies/owners/read",
"microsoft.directory/applicationPolicies/policyAppliedTo/read",
"microsoft.directory/applicationPolicies/basic/update",
"microsoft.directory/applicationPolicies/owners/update",
"microsoft.directory/servicePrincipals/create",
"microsoft.directory/servicePrincipals/delete",
"microsoft.directory/servicePrincipals/disable",
"microsoft.directory/servicePrincipals/enable",
"microsoft.directory/servicePrincipals/getPasswordSingleSignOnCredentials",
"microsoft.directory/servicePrincipals/synchronizationCredentials/manage",
"microsoft.directory/servicePrincipals/synchronizationJobs/manage",
"microsoft.directory/servicePrincipals/synchronizationSchema/manage",
"microsoft.directory/servicePrincipals/managePasswordSingleSignOnCredentials",
"microsoft.directory/servicePrincipals/appRoleAssignedTo/update",
"microsoft.directory/servicePrincipals/audience/update",
"microsoft.directory/servicePrincipals/authentication/update",
"microsoft.directory/servicePrincipals/basic/update",
"microsoft.directory/servicePrincipals/credentials/update",
"microsoft.directory/servicePrincipals/owners/update",
"microsoft.directory/servicePrincipals/permissions/update",
"microsoft.directory/servicePrincipals/policies/update",
"microsoft.directory/servicePrincipals/tag/update",
"microsoft.directory/signInReports/allProperties/read")

$rolePermissions = @{'allowedResourceActions'= $allowedResourceAction}
 
# Create new custom admin role
$customAdmin = New-AzureADMSRoleDefinition -RolePermissions $rolePermissions -DisplayName $displayName -Description $description -TemplateId $templateId -IsEnabled $true



# Get the user and role definition you want to link
$user = Get-AzureADUser -Filter "userPrincipalName eq 'think.cloud@freeiotcloud.com'"
$roleDefinition = Get-AzureADMSRoleDefinition -Filter "displayName eq 'Custom Application Support Administrator'"

# Get app registration and construct resource scope for assignment.
$appRegistration = Get-AzureADApplication -Filter "displayName eq 'MJDLABTEST'"
$resourceScope = '/' + $appRegistration.objectId

# Create a scoped role assignment
$roleAssignment = New-AzureADMSRoleAssignment -ResourceScope $resourceScope -RoleDefinitionId $roleDefinition.Id -PrincipalId $user.objectId




