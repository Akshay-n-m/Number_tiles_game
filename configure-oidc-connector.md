# commands to configure IAM OIDC provider 

```
$clusterName = "demo-cluster" 
```

```
$oidclssuer = aws eks describe-cluster --name $clusterName --query "cluster.identity.oidc.issuer" --output text 
$oidcld = ($oidclssuer -split "/")[-1] 
Write-Output "OIDC ID: $oidcld"
```

## Check if there is an IAM OIDC provider configured already

- $oidc_id = "your-oidc-id" # set your oidc_id
aws iam list-open-id-connect-providers | Select-String $oidc_id | ForEach-Object {
    ($_ -split "/")[3]
}
 

If not, run the below command

```
$clusterName = "demo-cluster" 

eksctl utils associate-iam-oidc-provider --cluster $clusterName --approve
```