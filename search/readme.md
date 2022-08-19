# Example of search web app by using Azure Maps

## Tools

- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)

## Deploy az

Execute the following bash commands:

```bash
# create Ressource Group
az group create --name spatial-geofence-dev-rg --location switzerlandnorth

# Create Azure Maps accounts (Geofence API requireses region=Global)
az maps account create --account-name spatial-geofence-dev-am --resource-group spatial-geofence-dev-rg --kind Gen2 --sku G2 --accept-tos
```

## Setup

Replace your account informations in the `interactive-search.html` file at the authOptions part on line 44 and 54.

Otherwise use this bash script lines:

```bash
# Get the Azure Maps secrets
PRIMARYKEY=$(az maps account keys list --account-name spatial-geofence-dev-am --resource-group spatial-geofence-dev-rg --output tsv --query "primaryKey") && \
CLIENTID=$(az maps account show --account-name spatial-geofence-dev-am --resource-group spatial-geofence-dev-rg --output tsv --query properties.uniqueId) && \
echo "ClientId=$CLIENTID SasKey=$PRIMARYKEY"

# Update the .html sample with the secretes
sed -i "s/CLIENT_ID/$CLIENTID/;s/SAS_PRIMARY_KEY/$PRIMARYKEY/" interactive-search.html
```