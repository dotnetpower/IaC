# IaC

```sql
+-------------------------------------------------------------+
|                        Azure Region: koreacentral           |
+-------------------------------------------------------------+

                ┌─────────────────────┐
                │ Resource Group:     │
                │      rg-hub         │
                └─────────────────────┘
                           │
             ┌─────────────┴──────────────┐
             │                            │
 ┌──────────────────────┐     ┌─────────────────────────┐
 │   Virtual Network    │     │     NAT Gateway         │
 │      vnet-hub        │◄────┤   (nat-gw-hub)          │
 └──────────────────────┘     └─────────────────────────┘
             │
             │
             ▼
 ┌────────────────────────────┐
 │ Private DNS Resolver       │
 │ - Inbound Endpoint         │
 │ - Outbound Endpoint        │
 └────────────────────────────┘

                           │
                         Peering
                           │
                           ▼

                ┌─────────────────────┐
                │ Resource Group:     │
                │     rg-spoke        │
                └─────────────────────┘
                           │
             ┌─────────────┴──────────────┐
             │                            │
 ┌──────────────────────┐      ┌─────────────────────────────┐
 │   Virtual Network    │      │ Azure Kubernetes Service    │
 │     vnet-spoke       │────▶│ (AKS Cluster with Azure CNI │
 │  (AKS + Node Subnet) │      │  Overlay Network Plugin)    │
 └──────────────────────┘      └─────────────────────────────┘
        │     ▲
        │     │
        └─────┘
      Outbound via
      NAT Gateway
```