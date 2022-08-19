# Example of geofence by using Azure Maps

## Tools

- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
- [geojson.io](https://geojson.io)
- [VS Code]()
  - [Extension: REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)

## Deploy az 

Execute the following bash commands:

```bash
# create Ressource Group
az group create --name spatial-geofence-dev-rg --location switzerlandnorth

# Create Azure Maps accounts (Geofence API requireses region=Global)
az maps account create --account-name spatial-geofence-dev-am --resource-group spatial-geofence-dev-rg --kind Gen2 --sku G2 --accept-tos

# Get the Azure Maps secrets
PRIMARYKEY=$(az maps account keys list --account-name spatial-geofence-dev-am --resource-group spatial-geofence-dev-rg --output tsv --query "primaryKey") && \
CLIENTID=$(az maps account show --account-name spatial-geofence-dev-am --resource-group spatial-geofence-dev-rg --output tsv --query properties.uniqueId) && \
echo "ClientId=$CLIENTID SasKey=$PRIMARYKEY"

# Update the .rest file with the Azure Map secrets
sed -i "s/AZUREMAPPRIMARYKEY/$PRIMARYKEY/;s/AZUREMAPCLIENTID/$CLIENTID/" geofenceSample.rest
```

## Play with the example

We use the geojson file [geofence.geojson](geofence.geojson) thats define 2 Polygon areas. Be aware of the `validyTime`, see [Azure Maps Geofencing](https://docs.microsoft.com/en-us/azure/azure-maps/geofence-geojson)

The file [geofenceSample.rest](geofenceSample.rest) with the VS Code Extension [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) can easy upload the geojson file and send the following request to get the udid thats identify the Operations target.

> Go to [geojson.io](https://geojson.io) to modify the file.

## Cleanup

```bash
# Delete resource groups
az group delete --yes --no-wait --name spatial-geofence-dev-rg
```


## docs

- [Azure Maps - Geofencing GeoJSON data](https://docs.microsoft.com/en-us/azure/azure-maps/geofence-geojson)
- [Azure Maps - Data V2 - Upload](https://docs.microsoft.com/en-us/rest/api/maps/data-v2/upload?tabs=HTTP)
- [Azure Maps - Spatial Geofence](https://docs.microsoft.com/en-us/rest/api/maps/spatial/get-geofence?tabs=HTTP)
- [Azure Maps - Pricing](https://azure.microsoft.com/de-de/pricing/details/azure-maps/)