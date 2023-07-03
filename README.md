# Blob Storage

## Introduction:

Blob Storage is a feature provided by Azure that offers scalable, secure, and highly available storage for various types of unstructured data such as images, videos, documents, backups, and logs. It allows you to store and retrieve large amounts of data from anywhere in the world, making it suitable for a wide range of applications.

## Key Concepts:

- A resource group is a logical container that holds Azure resources. It provides a way to organize and manage related resources together.
- A storage account is a logical entity in Azure that holds all of your Azure Storage data. It serves as a unique namespace for your storage resources.
- Containers are logical compartments within a storage account. You can think of them as folders that help organize and manage your blobs.
- Blobs are the actual data objects stored in Blob Storage. They can be files of any type or size, and they are organized within containers.

## Difference between Blob Storage and File System:

The main difference between Blob Storage and the file system of Linux/Windows/Mac is that Blob Storage provides a flat address space for storing data, whereas the file systems use a hierarchical directory structure. Blob Storage does not enforce a specific file structure or hierarchy, making it more flexible for storing unstructured data.

## Advantages of Blob Storage:

- Scalability: Blob Storage allows you to store and retrieve large amounts of data, scaling up as your storage needs grow.
- Durability and Redundancy: Blob Storage provides built-in redundancy options to ensure data durability and high availability.
- Security: Blob Storage offers various security features such as encryption, shared access signatures, and Azure Active Directory integration.
- Access from Anywhere: Blobs can be accessed from anywhere in the world using simple HTTP or HTTPS requests.

## Disadvantages of Blob Storage:

- Lack of Native File System Operations: Blob Storage does not support traditional file system operations like renaming or moving files. It requires the use of APIs or Azure CLI/PowerShell commands for management tasks.

- Additional Development Effort: Working with Blob Storage may require some additional development effort compared to using the native file systems of Linux/Windows/Mac.

## Different Tiers:

Blob Storage offers different tiers to optimize storage costs based on access patterns and durability requirements:

- Hot Access Tier: Optimized for frequently accessed data with slightly higher storage costs.

- Cool Access Tier: Optimized for infrequently accessed data with lower storage costs but higher data retrieval costs.

- Archive Access Tier: Optimized for rare access, long-term retention, and lowest storage costs, with higher data retrieval costs and longer retrieval times.

## Redundancy Types:

- LRS (Locally Redundant Storage): Data is replicated within a single storage scale unit in a single region, providing high durability.

- ZRS (Zone-Redundant Storage): Data is replicated synchronously across multiple availability zones within a region, increasing data availability.

- GRS (Geo-Redundant Storage): Data is replicated asynchronously to a secondary region, providing a higher level of durability and availability.

- RA-GRS (Read-Access Geo-Redundant Storage): Same as GRS, with the additional capability of read access to the replicated data in the secondary region.

- GZRS (Geo-Zone-Redundant Storage): Data is replicated synchronously across multiple regions within a single zone, offering higher durability and availability.

- RA-GZRS (Read-Access Geo-Zone-Redundant Storage): Same as GZRS, with the additional capability of read access to the replicated data in the secondary region.

![redundancy img](azure-storage-replication-options.png)

## Cost Comparison:

To compare the cost of different redundancy types and available options in Azure, you can use the Azure Pricing Calculator. By selecting the desired region, redundancy type, and storage capacity, you can estimate the cost for each option and compare them based on your requirements.

## Selecting Redundancy Type on Azure Portal:

To select the redundancy type for your Azure Blob Storage, follow these steps:

1. Go to the Azure Portal (portal.azure.com) and navigate to your storage account.

2. In the storage account overview, click on "Containers" to view your containers.

3. Select the container for which you want to set the redundancy type.

4. In the container overview, navigate to the "Settings" section.

5. Click on "Access policy" and select the desired redundancy type from the available options.

6. Save the changes to apply the selected redundancy type to the container.

## Command-line examples using Azure CLI:

To install azure commands on linux here is the command:
    curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

`az` Every command starts with this in Azure cli

`az login` -> Takes you to a browers to log in and give back a JSON array which shows your information. **Do NOT put this on github!**

    # This command creates the storage account. If it has worked you get a large object:

    az storage account create --name tech241elenastorage --resource-group tech241 --location uksouth --sku Standard_LRS
    
    # Lists all of the storage accounts for the resource group
    az storage account list --resource-group tech241

    # Choose which bits you want to display
    az storage account list --resource-group tech241 --query "[].{Name:name, Location:location, Kind:kind}" --output table

    # Make a container
    az storage container create --account-name tech241elenastorage --name testcontainer

    # Upload a blob to a container

    touch test.txt # Create an empty file
    nano test.txt # Put in a line just to make it not empty

    az storage blob upload \ 
    --account-name tech241elenastorage \ --container-name testcontainer \ 
    --name newname.txt \ 
    --file test.txt \ 
    --auth-mode login

    # Check if the blob is in the container

    az storage blob list \
    --account-name tech241elenastorage \
    --container-name testcontainer \
    --output table \
    --suth-mode login

To make it privite go into storage account on azure portal. Then containers and click on the test container. Within there will ba a file called newname.txt. Click on it and it has the url.

The url is private and shows that it doesnt exist even though it does to prevent hackers.

To stop this you can change the access level.

## Protecting Blob Access:

To secure access to your blobs, you can make them private by modifying the access level:

1. Go to the Azure Portal and navigate to your storage account.

2. In the storage account overview, click on "Containers" to view your containers.

3. Select the container that contains the blob you want to protect.

4. In the container overview, navigate to the "Access policy" section.

5. Change the access level to "Private" to restrict access to the blob.

6. Save the changes to apply the access level settings.

Please note that the URL of a private blob will return a 404 error if accessed without proper authorization.