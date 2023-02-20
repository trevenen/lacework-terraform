# lacework-terraform
sample lacework install with terraform

To wrap a Lacework Helm file install in Terraform, you can use the helm_release resource in the Helm provider for Terraform. Here are the steps you can follow:

First, you need to ensure that you have the Helm provider for Terraform installed. You can do this by adding the following code to your Terraform configuration:
terraform
Copy code
provider "helm" {
  version = "2.2.0"
}
This will download and install the Helm provider.

Next, you need to create a helm_release resource for your Lacework Helm chart installation. Here is an example code block you can use:
terraform
Copy code
resource "helm_release" "lacework" {
  name       = "lacework"
  repository = "https://helm.lacework.net/"
  chart      = "lacework"
  version    = "1.24.1"
  namespace  = "lacework"

  set {
    name  = "accessToken"
    value = var.lacework_access_token
  }

  set {
    name  = "satelliteName"
    value = var.lacework_satellite_name
  }
}
In this example, we are creating a Helm release resource named "lacework" that will install the Lacework Helm chart from the official Lacework Helm repository. We are also passing two values using the set block, which will be used by the Lacework chart to configure the installation. These values are defined as variables (e.g., var.lacework_access_token) so that they can be set in the Terraform plan.

Finally, you can add any necessary variables to your Terraform plan, like this:
terraform
Copy code
variable "lacework_access_token" {
  type = string
}

variable "lacework_satellite_name" {
  type = string
}
In this example, we are defining two variables, lacework_access_token and lacework_satellite_name, which will be used by the helm_release resource to configure the Lacework installation.

Once you have completed these steps, you can run terraform apply to install the Lacework Helm chart. Terraform will create the Helm release resource and configure the installation using the values you specified in the set blocks.
