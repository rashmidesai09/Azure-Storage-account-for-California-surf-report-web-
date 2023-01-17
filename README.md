# Azure Storage account for Goa surf report web

## Project Overview : 

Create a storage account for a southern Goan surf report web app. The surf report site should let users upload photos and videos of local beach conditions. Viewers will use the content to help them choose the beach with the best surfing conditions
 
### List of design and feature goals are -

- Video content must load quickly.
- The site must handle unexpected spikes in upload volume.
- Outdated content must be removed as surf conditions change so the site always shows current conditions.

#### Create a storage account using Azure portal as follows -
1. Sign in to the Azure portal.

2. On the resource menu, or from the Home page, select Storage accounts. The Storage accounts pane appears.

3. On the command bar, select Create. The Create a storage account pane appears.

##### Basics Tab screenshot -

<img width="700" alt="image" src="https://user-images.githubusercontent.com/97893144/212598573-27e161d6-7ce6-4ea6-a19b-afec982e569f.png">

Details -

Storage account name -
This should have a unique name as it will be used to generate the public URL to access the data in the account.
The name must be unique across all existing storage account names in Azure. Names must have 3 to 24 characters and can contain only lowercase letters and numbers.

Region - 	Location that is nearby from the dropdown list is selected.

Performance	- Standard option decides the type of disk storage used to hold the data in the Storage account. Standard uses traditional hard disks, and Premium uses solid-state drives (SSD) for faster access.

Redundancy	- Locally redundant storage (LRS) from the dropdown list is selected. In this case, the images and videos quickly become out-of-date and are removed from the site. As a result, there's little value to paying extra for global redundancy. If a catastrophic event results in data loss, there is possibilty to restart the site with fresh content from users.


##### Advanced Tab screenshot -

<img width="700" alt="image" src="https://user-images.githubusercontent.com/97893144/212598841-e6f262a4-2183-4c13-bb9f-2ef30979b924.png">

Require secure transfer for REST API operations -	Checking this setting controls whether HTTP can be used for the REST APIs that access data in the storage account. Setting this option to enable forces all clients to use SSL (HTTPS). Most of the time, set secure transfer to enable; using HTTPS over the network is considered a best practice.

Enable blob public access	- Check this to allow clients to read data in that container without authorizing the request.

Enable storage account key access	- Check this to allow clients to access data via SAS.

Default to Azure Active Directory authorization in the Azure portal -	Uncheck this as Clients are public and are not part of an Active Directory.

Minimum TLS version	- Select Version 1.2 from dropdown list. TLS 1.2 is a secure version of TLS, and Azure Storage uses it on public HTTPS endpoints. TLS 1.1 and 1.0 are supported for backwards compatibility. 

Permitted scope for copy operations -	Accept default

<img width="700" alt="image" src="https://user-images.githubusercontent.com/97893144/212598883-6b226cb6-5163-4d4b-80b4-c401d9c7d5ad.png">

Enable hierarchical namespace -	Uncheck this as Data Lake hierarchical namespace is for big-data applications that aren't relevant to this project.

<img width="700" alt="image" src="https://user-images.githubusercontent.com/97893144/212598911-b0638a5a-6999-499a-8262-58ca850426d5.png">

Enable SFTP	 - Uncheck asSFTP is disabled by default and isn't relevant to this implementation.

Enable network file system v3 -	Uncheck (default).

Allow cross-tenant replication -	Uncheck as Active Directory is not being used for this implementation.

Access tier	Hot - This setting is only used for Blob storage. The Hot access tier is ideal for frequently accessed data; the Cool access tier is better for infrequently accessed data. This setting only sets the default value. 
When Blob is created, set a different value for the data. In this case, we want the videos to load quickly, so we use the high-performance option for our blobs.

Enable large file shares	- Uncheck as Large file shares provide support up to a 100 TiB, however this type of storage account can't convert to a Geo-redundant storage offering, and upgrades are permanent.
If Enable large file shares is selected, it will enforce additional restrictions, and Azure files service connections without encryption will fail, including scenarios using SMB 2.1 or 3.0 on Linux. Because Azure storage doesn't support SSL for custom domain names, this option cannot be used with a custom domain name.

##### Networking Tab screenshot -

<img width="700" alt="image" src="https://user-images.githubusercontent.com/97893144/212598969-75fc53dd-c37a-46b3-bcbe-c01ada679731.png">

Connectivity method	Enable public access from all networks -  We want to allow public Internet access. Our content is public facing, and we need to allow access from public clients.

Routing preference	Microsoft network routing -We want to make use of the Microsoft global network that is optimized for low-latency path selection.

##### Data Protection Tab screenshot -

<img width="700" alt="image" src="https://user-images.githubusercontent.com/97893144/212599105-58c8a769-5fbd-46da-b6c6-7b107d17efd2.png">

Enable point-in-time restore for containers -	Uncheck as Not necessary for this implementation.

Enable soft delete for blobs	- Uncheck as Soft delete lets you recover blob data in cases where blobs or blob snapshots are deleted accidentally or overwritten.

Enable soft delete for containers -	Uncheck as Soft delete lets you recover your containers that are deleted accidentally.

Enable soft delete for file shares -	Uncheck as File share soft delete lets you recover your accidentally deleted file share data more easily.

Enable versioning for blobs -	Uncheck, not necessary for this implementation.

Enable blob change feed	 - Uncheck, not necessary for this implementation.

Enable version-level immutability support	- Uncheck this as it is not necessary for this implementation.

##### Encryption Tab and Tags screenshot -

<img width="700" alt="image" src="https://user-images.githubusercontent.com/97893144/212599163-ff233ed2-8715-47e9-befb-4acba2f9c05d.png">

Accept the defaults.

<img width="700" alt="image" src="https://user-images.githubusercontent.com/97893144/212599241-9109fcb3-13ca-454d-9fd8-d917edd0025a.png">

This is to associate key/value pairs with the account for  categorization to determine if a feature is available to selected Azure resources.
Here we are leaving it empty.

##### Review and Create -

<img width="700" alt="image" src="https://user-images.githubusercontent.com/97893144/212599298-ef3f36f9-5788-46ec-9841-fd15708ec985.png">

<img width="700" alt="image" src="https://user-images.githubusercontent.com/97893144/212599343-94e117d8-5d62-41f2-bda2-455fd14cfb24.png">

<img width="700" alt="image" src="https://user-images.githubusercontent.com/97893144/212599364-a919c1b5-c588-4c17-b6a7-529376c86cb5.png">

This option is to validate all options and to ensure all the required fields are selected. If there are issues, this tab will identify them so as to correct them.
When validation passes successfully, select Create to deploy the storage account.

##### Deployment -

<img width="700" alt="image" src="https://user-images.githubusercontent.com/97893144/212601250-c399d472-b4e5-4699-aed3-335189db01b1.png">

When deployment is complete, which may take up to two minutes, select Go to resource to view Essential details about new storage account as above.
 
<img width="900" alt="image" src="https://user-images.githubusercontent.com/97893144/212601384-279ff4a8-4a10-4be6-ad79-f18cffbd3815.png">

<img width="900" alt="image" src="https://user-images.githubusercontent.com/97893144/212601426-a5b99293-0860-4120-964d-1b737c432238.png">


Final comments - A storage account with settings driven by business requirements has been created successfully. 

The typical flow for creating a storage account is: first analyze your data and goals, and then configure the storage account options to match.
