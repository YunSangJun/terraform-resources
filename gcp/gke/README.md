# GKE Cluster

## Prerequisites

1. Enabling the following APIS.
- Compute Engine API
- Kubernetes Engine API

Refer a [Enabling APIs](https://cloud.google.com/apis/docs/getting-started#enabling_apis) guide.

2. Creating a service account

Create a service account with the following roles.
- Kubernetes Engine Admin
- Compute Network Admin
- Service Account User

Refer a [Create a service account](https://cloud.google.com/docs/authentication/production#create_service_account) guide.

Export the service account as json file when creating.
The json file will be used the next step.

## Clone terraform code for GKE

```
$ git clone https://github.com/YunSangJun/terraform-resources
$ cd terraform-resources/gcp/gke
```

## Initialize Terraform workspace

```
$ terraform init
...

Terraform has been successfully initialized!
```

## Provision GKE cluster

1. Set your environment variables

    ```
    ## "GOOGLE_APPLICATION_CREDENTIALS" is a file's path exported from service account.
    export GOOGLE_APPLICATION_CREDENTIALS="REPLACE_ME"
    export PROJECT_ID="REPLACE_ME"
    export REGION="REPLACE_ME"

    ## e.g
    export GOOGLE_APPLICATION_CREDENTIALS="/User/sjyun/.gcp/gke-service-account.json"
    export PROJECT_ID="my-project"
    export REGION="asia-northeast3"
    ```

2. Verify before provision

    ```
    $ terraform plan \
        -var "project_id=$PROJECT_ID" \
        -var "region=$REGION" \
        -var "gke_num_nodes=1"
    ...

3. Run "terraform apply" command with the enviroment variables

    ```
    $ terraform apply \
        -var "project_id=$PROJECT_ID" \
        -var "region=$REGION" \
        -var "gke_num_nodes=1"
    ...
    
    Outputs:
      + kubernetes_cluster_name = "my-project-gke"
      + region                  = "asia-northeast3"

    Apply complete! Resources: 4 added, 0 changed, 0 destroyed.
    ```

## Destroy GKE cluster

```
$ terraform destroy \
    -var "project_id=$PROJECT_ID" \
    -var "region=$REGION"
...

Destroy complete! Resources: 4 destroyed.
```
