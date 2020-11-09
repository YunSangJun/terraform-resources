# GKE Cluster

## Prerequisites

Create a service account with the following roles.
- Kubernetes Engine Cluster Admin
- Compute Network Admin
- Service Account User

Refer a [Create a service account](https://cloud.google.com/docs/authentication/production#create_service_account) guide.

After creating the service account export as json file.

## Initialize Terraform workspace

```
$ terraform init

Initializing the backend...

Initializing provider plugins...
- Finding latest version of hashicorp/google...
- Installing hashicorp/google v3.46.0...
- Installed hashicorp/google v3.46.0 (signed by HashiCorp)
...

* hashicorp/google: version = "~> 3.46.0"

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

        An execution plan has been generated and is shown below.
        Resource actions are indicated with the following symbols:
        + create

        Terraform will perform the following actions:
        ...

        Plan: 4 to add, 0 to change, 0 to destroy.

        Changes to Outputs:
        + kubernetes_cluster_name = "booming-pride-290113-gke"

        Do you want to perform these actions?
        Terraform will perform the actions described above.
        Only 'yes' will be accepted to approve.

        Enter a value: yes  
        ...

        google_compute_network.vpc: Creating...
        ...

        Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

        Outputs:

        kubernetes_cluster_name = booming-pride-290113-gke
        region = asia-northeast3
        ```

## Destroy GKE cluster

```
$ terraform destroy \
    -var "project_id=$PROJECT_ID" \
    -var "region=$REGION"

An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:
...

Do you really want to destroy all resources?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.

  Enter a value: yes
...

Destroy complete! Resources: 3 destroyed.
```