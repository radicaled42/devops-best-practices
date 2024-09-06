# Scale to Zero an AWS EKS Cluster

Scaling the master nodes of an EKS (AWS Kubernetes Cluster) to zero is not possible, as these nodes are managed by AWS. However, you can scale the worker node groups to zero, effectively minimizing the resource usage of your cluster.

## Manually Scale to Zero a Cluster

1. Install AWS CLI: Download and install the AWS CLI tool from [here](https://aws.amazon.com/cli/).
2. Install eksctl: Download and install eksctl from [here](https://eksctl.io/).
3. Log in to your AWS account using a profile or AWS environment variables.
4. Run the following command for each nodegroup in your cluster:

```
    eksctl scale nodegroup --cluster=<CLUSTER_NAME> --nodes=0 --name=<NODEGROUP_NAME> --nodes-min=0 --nodes-max=1
```

5. Repeat the command for each additional nodegroup you have.
6. To scale up the cluster, run the following command:

```
    eksctl scale nodegroup --cluster=<CLUSTER_NAME> --nodes=<NUMBER_OF_NODES> --name=<NODEGROUP_NAME> --nodes-min=0 --nodes-max=<NUMBER_OF_NODES>
```

**Note**: Ensure the nodes are tainted (marked as unschedulable) before scaling down, to prevent pods from automatically migrating to other node groups. If the nodes are not tainted, workloads may move unexpectedly.

## Scale to Zero a Cluster Using a GitHub Action

A GitHub action can automate the process of scaling your EKS nodegroups to zero, based on a cron schedule. Here’s an example of setting up a cron-based stop/start for an EKS nodegroup.

### Requirements:

1. Set up an IAM user with no console access and only the necessary permissions to manage EKS.
2. Configure the ACCESS_KEY, SECRET_ACCESS_KEY, and AWS_REGION secret variables in GitHub:
    1. Navigate to your repository settings.
    2. Select Secrets and variables.
    3. Select Actions.
    4. Create New repository secrets for each of the variables.

### GitHub Action Example:

```yaml
name: Cron-Based EKS Control
on:
  schedule:
    - cron: "0 5 * * 1-6" # 05:00 GMT - 02:00 GMT-3 - 00:00 EST
    - cron: "0 11 * * 1-5" # 11:00 GMT - 08:00 GMT-3 - 07:00 EST

jobs:
  action:
    name: Cron-Based EKS Control
    runs-on: ubuntu-latest

    steps:
      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.ACCESS_KEY }}
          aws-secret-access-key: ${{ secrets.SECRET_ACCESS_KEY }}
          aws-region: ${{ secrets.AWS_REGION }}

      - name: Install and configure kubectl
        run: |
          VERSION=$(curl --silent https://storage.googleapis.com/kubernetes-release/release/stable.txt)
          curl https://storage.googleapis.com/kubernetes-release/release/$VERSION/bin/linux/amd64/kubectl --progress-bar --location --remote-name
          chmod +x kubectl
          sudo mv kubectl /usr/local/bin/
          aws eks update-kubeconfig --region ${{ secrets.AWS_REGION }} --name <CLUSTER_NAME>

      - name: Install EKSCTL
        run: |
          # for ARM systems, set ARCH to: `arm64`, `armv6`, or `armv7`
          ARCH=amd64
          PLATFORM=$(uname -s)_$ARCH
          curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"
          tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz
          sudo mv /tmp/eksctl /usr/local/bin

      - name: Trigger Step to Shutdown Cluster
        if: github.event.schedule == '0 5 * * 1-6'
        run: |
          echo "Scaling nodegroup down to zero nodes"
          eksctl scale nodegroup --cluster=<CLUSTER_NAME> --nodes=0 --name=<NODEGROUP_NAME> --nodes-min=0 --nodes-max=1

      - name: Trigger Step to Start Up Cluster
        if: github.event.schedule == '0 11 * * 1-5'
        run: |
          echo "Scaling nodegroup up to the desired number of nodes"
          eksctl scale nodegroup --cluster=<CLUSTER_NAME> --nodes=<NUMBER_OF_NODES> --name=<NODEGROUP_NAME> --nodes-min=0 --nodes-max=<NUMBER_OF_NODES>
```

If you don't want to provide full access to the EKS Control user, use the following IAM policy:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "eks:DescribeCluster",
                "eks:DescribeNodegroup",
                "eks:UpdateNodegroupConfig",
                "eks:ListNodegroups",
                "eks:ListClusters",
                "cloudformation:DescribeStacks",
                "iam:PassRole",
                "ec2:DescribeInstances",
                "ec2:DescribeSubnets",
                "ec2:DescribeSecurityGroups"
            ],
            "Effect": "Allow",
            "Resource": [
                "arn:aws:eks:us-east-2:223007967604:cluster/<CLUSTER_NAME>",
                "arn:aws:eks:us-east-2:223007967604:nodegroup/<CLUSTER_NAME>/<NODEGROUP_NAME>/*"
            ]
        },
        {
            "Action": "iam:PassRole",
            "Effect": "Allow",
            "Resource": "*"
        },
        {
            "Action": "cloudformation:ListStacks",
            "Effect": "Allow",
            "Resource": "arn:aws:cloudformation:us-east-2:223007967604:stack/*/*"
        },
        {
            "Action": "autoscaling:*",
            "Effect": "Allow",
            "Resource": "*"
        },
        {
            "Action": "cloudwatch:PutMetricAlarm",
            "Effect": "Allow",
            "Resource": "*"
        },
        {
            "Action": [
                "ec2:DescribeAccountAttributes",
                "ec2:DescribeAvailabilityZones",
                "ec2:DescribeImages",
                "ec2:DescribeInstanceAttribute",
                "ec2:DescribeInstances",
                "ec2:DescribeKeyPairs",
                "ec2:DescribeLaunchTemplateVersions",
                "ec2:DescribePlacementGroups",
                "ec2:DescribeSecurityGroups",
                "ec2:DescribeSpotInstanceRequests",
                "ec2:DescribeSubnets",
                "ec2:DescribeVpcClassicLink"
            ],
            "Effect": "Allow",
            "Resource": "*"
        },
        {
            "Action": [
                "elasticloadbalancing:DescribeLoadBalancers",
                "elasticloadbalancing:DescribeTargetGroups"
            ],
            "Effect": "Allow",
            "Resource": "*"
        },
        {
            "Action": "iam:CreateServiceLinkedRole",
            "Condition": {
                "StringEquals": {
                    "iam:AWSServiceName": "autoscaling.amazonaws.com"
                }
            },
            "Effect": "Allow",
            "Resource": "*"
        }
    ]
}
```


By radicaled42
