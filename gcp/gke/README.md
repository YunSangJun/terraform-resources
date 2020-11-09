# GKE Cluster

## Prerequisites

Create a service account with the following roles.
- Kubernetes Engine Cluster Admin
- Compute Network Admin
- Service Account User

Refer a [Create a service account](https://cloud.google.com/docs/authentication/production#create_service_account) guide.

Export the service account as json file after creating.

## Initialize Terraform workspace

```
$ terraform init
...

Terraform has been successfully initialized!
```

## Provision GKE cluster

1. Set your environment

        ## "GOOGLE_APPLICATION_CREDENTIALS" is a file's path exported from service account.
        ```
        export GOOGLE_APPLICATION_CREDENTIALS="REPLACE_ME"
        export PROJECT_ID="REPLACE_ME"
        export REGION="REPLACE_ME"

        ## e.g
        export GOOGLE_APPLICATION_CREDENTIALS="~/.credential/gke-service-account.json"
        export PROJECT_ID="my-project"
        export REGION="asia-northeast3"
        ```

2. Run "terraform apply" command with the enviroment

        ```
        $ terraform apply \
            -var "project_id=$PROJECT_ID" \
            -var "region=$REGION" \
            -var "gke_num_nodes=1" \
            -var "gke_machine_type=e2-standard-2"
        ...
        
        Outputs:
          + kubernetes_cluster_name = "my-project-gke"
          + region                  = "asia-northeast3"
        ```

## Destroy GKE cluster

```
$ terraform destroy \
    -var "project_id=$PROJECT_ID" \
    -var "region=$REGION"
...

Destroy complete! Resources: 3 destroyed.
```
