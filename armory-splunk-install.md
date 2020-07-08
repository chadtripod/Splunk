description: >
  Configure the AWS Provider for Spinnaker and connect to an EKS cluster.
---


Need help setting this up? - For a guided tutorial, see the [video walkthrough](#aws-quickstart-step-2-video) at the bottom of this page.

{{% alert title="Note" %}}This guide assumes that Spinnaker is installed with Halyard, not Operator.{{% /alert %}}

## Prerequisites

Before you start, ensure that have completed the following requirements:
* Finish [AWS QuickStart Step 1]({{< ref "Armory-Spinnaker-Quickstart-1" >}}).
* Have access to the Kubernetes cluster you would like to deploy to, and you need cluster admin permissions on that Kubernetes cluster.
* Have `kubectl` installed on your local workstation have the context set to the EKS cluster you want to deploy to.

    Running the following command from your local machine should return the namespaces for the EKS cluster you want to deploy to.

  ```bash
  kubectl get ns
  ```

* Have a way to copy files from your local workstation to the Minnaker VM, such as `scp`.


## First: Configure the AWS Provider for Spinnaker

![No CREATE Permission](/images/AWS-Deploy-Spinnaker.png)

### Adding AWS Role to Spinnaker through Halyard configuration.  Note AWS account name is within Spinnaker and will appear in UI ###

**NOTE**: You **MUST** configure the regions that Spinnaker can deploy to in the `hal` command below.

The Account name is arbitrary and should be a name that is an identifiable.  The name is visable in Spinnaker UI.  The following examples use `aws-dev-1`.

1. Set environment variables for halyard command:

   ```bash
   export AWS_ACCOUNT_NAME=aws-dev-1 \
   export ACCOUNT_ID=[YOUR_ACCOUNT_ID] \
   export ROLE_NAME=role/Spinnaker-Managed-Role
   ```

2. Add the AWS provider account to Spinnaker:

   ```bash
   hal config provider aws account add ${AWS_ACCOUNT_NAME} \
     --account-id ${ACCOUNT_ID} \
     --assume-role ${ROLE_NAME} \
     --regions us-east-1,us-west-2
   ```

3. Enable the AWS provider:

   ```bash
   hal config provider aws enable
   ```
## Congratulations!  
You have configured the Spinnaker AWS Provider and Kubernetes Account for EKS.  You can now deploy to EC2, ECS, Fargate, and EKS.  Lets build some pipelines in [AWS QuickStart Step 3]({{< ref "Armory-Spinnaker-Quickstart-3" >}}).

## AWS QuickStart Step 2 Video
{{< youtube XBdc0z-xdS0 >}}
