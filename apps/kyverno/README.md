# kyverno

## Cluster Filter
We allow to filter policies based on cluster metadata. Metadata includes:
- Cluster Name
- Cluster Region (us|eu|ap|au)
- Cluster Tier (dev|qa|sand|prod)
- Cluster Provider (azure|aws)

Filtering is done using `clusterFilter` field in `ClusterPolicy` resource(on same level as metadata and spec fields).
Filtering supports both include and exclude. List of supported fields:
- `clusterName` or `excludeClusterName`
- `clusterRegion` or `excludeClusterRegion`
- `clusterTier` or `excludeClusterTier`
- `clusterProvider` or `excludeClusterProvider`

Each filed is independent and can be used separately. Or you can combine them to create more complex filters.
All filters will be `and`-ed together. If no clusterFilter is specified, policy will be applied to all clusters.

```yaml
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: cluster-policy
spec:
    ...
clusterFilter:  # this example deploys policy to clusters in us region but not in prod
  clusterRegion: "us"
  excludeClusterTier: "prod"
```
