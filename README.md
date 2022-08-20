# spatial-analytics-example

Dis Repository shows how to handle with Azure Maps to get first expirence with the SDK.

Examples:
- A simple local web app written in javascript to demonstrate the interactive search experience. See the [search readme.md](/search/readme.md)
- A examples thats use the REST api for spatial analytics. See the [geofence readme.md](/geofence/readme.md)

> Be aware of the unique azure names. Best is to replace all following names with your unique one: spatial-geofence-dev-am, spatial-geofence-dev-rg

# docs

Some kickstart Background information about Azure Maps

- [Azure Maps marketing information](https://azure.microsoft.com/en-us/services/azure-maps/)
- [Azure Maps docs](https://docs.microsoft.com/en-us/azure/azure-maps/about-azure-maps)
- [Azure Maps - Pricing](https://azure.microsoft.com/en-us/pricing/details/azure-maps/)

# az cheat sheet

```bash
# Interactive Login / set default subscription / logout
az login
az account set --subscription "your-subscription"
az logout --username "your-email"

# list locations
az account list-locations -o table

# Azure Maps commands help
az maps --help
```

