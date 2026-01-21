# Azure Policy Lab

# Overview

In this lab, I'll demonstrate how to strengthen governance across an Azure environment by working with Azure Policy. I'll create and assign policies to enforce organizational standards, apply and manage resource tags for better organization and cost visibility, and configure resource locks to protect assets from accidental changes or deletion.

# Create Resource Group

1. Navigate to the ‘**Resource** **Manager**’ and create a new resource group.
2. In the Tags tab, create a ‘**Cost** **Center**’ tag with the value ‘**000**’.
3. Select ’**Review + Create’** and then select **Create**.
    
    ![image.png](/image.png)
    

# Assign Policy to Resource Group

1. Navigate to the ‘**Policy**’ portal.
2. In the blades section, click on ‘**Authoring**’ > ‘**Definitions**’.
3. Search for the ‘**Require a tag and its value on resources’** built-in tag.
    
    ![image.png](/image%201.png)
    
4. Select it and click ‘**Assign** **Policy**’.
5. In the ‘**Scope**’ section, select your subscription and your resource group.
    
    > The ‘**Exclusions**’ setting allows you to exclude certain resources from being tagged within the resource group.
    > 
6. You can leave the policy definition as the default.
7. You can keep the default ‘**Assignment** **Name**’ or make it more specific, such as ‘**Require Cost Center tag and its value on resources**.’
8. Go to the ‘**Parameters**’ tab and input the tag that should be enforced on resources. 
    
    ![image.png](/image%202.png)
    
9. Click ‘**Review + Create**’ and create the policy. 

## Testing the Policy

1. To test the policy, we will attempt to create a resource within the resource group. 
2. Navigate to ‘**Storage** **Center**’ and create a new storage account.
3. Make sure it is under the correct subscription and resource group.
4. Give it a unique name.
5. Click on ‘**Review** **+** **Create**’ and click Create.
6. You should get an error when attempting to create the resource because you did not assign a tag to it.
    
    ![image.png](/image%203.png)
    

# Apply Tagging with Azure Policy

1. Navigate to the ‘**Policy**’ portal > ‘**Authoring**’ blade > ‘**Assignments**’.
2. Delete the previous policy we assigned.
    
    ![image.png](/image%204.png)
    
3. Click ‘**Assign** **Policy**’.
4. Set the scope to your subscription and resource group.
5. In the ‘Policy Definitions’ setting, search for and assign the ‘Inherit a tag from the resource group if missing’ policy.
6. You can leave the ‘Policy Definition’ and ‘Assignment Name’ the same or make them more detailed.
7. In the ‘**Parameters**’ tab, add the ‘Cost Center’ tag.
8. In the ‘**Remediation**’ tab, check the ‘**Create a remediation task**’.
    
    > By default, the policy only applies to newly created resources. The Remediation task allows existing resources to inherit the tag from the resource group.
    > 
9. In the ‘**Managed** **Identity**’ tab, the setting ‘**Create** **a** **Managed** **Identity**’ should be enabled by default.
    
    > A managed identity is required with the contributor permissions so that resource tags can be modified by Azure on your behalf.
    > 
10. Click on ‘**Review** **+** **Create**’ and create the assignment.

## Testing Policy Assignment

1. Navigate to the ‘**Storage** **Center**’ and click create.
2. Ensure it's under the proper subscription and resource group.
3. Give it a unique name.
4. Leave everything as default and go to the ‘**Review** **+** **Create**’ tab and click create.
5. Once the resource is delpoyed click ‘Go to resource’ and click on the ‘**Tags**’ blade. The storage account should have inherited the tag of the resource group.
    
    ![image.png](/image%205.png)
    

# Configuring Resource Lock

1. Navigate to your resource group > under the ‘**Settings**’ blade select ‘**Locks’**.
2. Click ‘**Add**’, then give the lock a name and assign it the ‘**Delete**’ lock type.
    
    > The ‘**delete**’ lock type prevents the deletion of a resource, and the '**read-only**' lock prevents modification.
    >
3. Click ‘**OK**’ to create the lock.
4. In the ‘**Overview**’ blade, click ‘**Delete** **Resource** **Group**’. 
5. In the new window, enter the resource group name and click ‘**Delete**’.
6. If you properly created the lock, you should get an error stating the deletion failed.
    
    ![SCR-20260120-sevr.png](/SCR-20260120-sevr.png)
    
    > You will need to remove the lock if you’d like to delete the resource group or any resource within it.
    > 

# Takeaways

1. Tags are metadata that can be used to label resources. 
2. Policies are used to enforce governance across your Azure environment.
3. You can assign policies at different scopes, such as the Management Group, Subscription, Resource Group, and Resource.
4. You can either use Microsoft’s existing policies or create your own.
5. The remediation task is used to bring the existing resources into compliance.
6. A managed identity is required for the remediation task to modify resource tags on your behalf.
7. Locks can be used to prevent accidental deletions and override user permissions.

Microsoft's Wite-up: https://github.com/MicrosoftLearning/AZ-104-MicrosoftAzureAdministrator/blob/master/Instructions/Labs/LAB_02b-Manage_Governance_via_Azure_Policy.md
