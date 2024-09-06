# Scale to zero a AWS Cluster

Actually its not possible to scale to zero an EKS (AWS Kubernetes Cluster) given that the master nodes are manage by AWS.
What you can do is to scale to zero the nodegroups.

## Manually scale to zero a cluster

1. Install AWS Cli (https://aws.amazon.com/cli/)
2. Install EKSCTL (https://eksctl.io/)
3. Login to you AWS account, by using a profile or a AWS environment variables
4. Run the following command:

```
eksctl scale nodegroup --cluster=<CLUSTER_NAME> --nodes=0 --name=<NODEGROUP_NAME> --nodes-min=0 --nodes-max=1
```
5. Repeat with any number of nodes you have
6. To scale up the cluster run the following command.

```
eksctl scale nodegroup --cluster=<CLUSTER_NAME> --nodes=<NUMBER_OF_NODES > 0> --name=<NODEGROUP_NAME> --nodes-min=0 --nodes-max=<NUMBER_OF_NODES >= nodes>
```
   
**Note**: make sure the nodes are tainted, otherwise the pods will migrate to other nodegroups.

## Scale to zero a cluster using a github action

A github action will follow the same principle as doing it manually.  
In this example I set up a cron based stop/start of an EKS nodegroup.

You will need the following:
1. Set up an IAM user with no console access and only access to EKS
2. Configure the ACCESS_KEY, SECRET_ACCESS_KEY and AWS_REGION secret variables on github
   1. Navigate to your repo setting
   2. Select `Secrets and variables`
   3. Select `Actions`
   4. Create `New repository secrets` with each of the variables

```
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
          curl https://storage.googleapis.com/kubernetes-release/release/$VERSION/bin/linux/amd64/kubectl \
            --progress-bar \
            --location \
            --remote-name
          chmod +x kubectl
          sudo mv kubectl /usr/local/bin/
          aws eks update-kubeconfig --region ${{ secrets.AWS_REGION }} --name <CLUSTER_NAME>

      - name: Install EKSCTL
        run: |
          # for ARM systems, set ARCH to: `arm64`, `armv6` or `armv7`
          ARCH=amd64
          PLATFORM=$(uname -s)_$ARCH
          curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"
          tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz
          sudo mv /tmp/eksctl /usr/local/bin

      - name: Trigger Step to Shutdown cluster
        if: github.event.schedule == '0 5 * * 1-6'
        run: |
          echo "This step will be run on during the shutdown"
          eksctl scale nodegroup --cluster=<CLUSTER_NAME> --nodes=0 --name=<NODEGROUP_NAME> --nodes-min=0 --nodes-max=1
          ...

      - name: Trigger Step to Start Up Cluster
        if: github.event.schedule == '0 11 * * 1-5'
        run: |
          echo "This step will be run during the startup"
          eksctl scale nodegroup --cluster=<CLUSTER_NAME> --nodes=<NUMBER_OF_NODES > 0> --name=<NODEGROUP_NAME> --nodes-min=0 --nodes-max=<NUMBER_OF_NODES >= nodes>
          ...
```

If you don't want to provide full access EKS Control user, you can use the following policy:

```
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
                "arn:aws:eks:us-east-2:223007967604:cluster/<CLUSTER_NAME>/<NODEGROUP_NAME>/*",
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
