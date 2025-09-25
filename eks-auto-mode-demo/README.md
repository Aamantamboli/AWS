# Amazon EKS Auto Mode: A Practical Demonstration
-----

### 1\. Practical Demonstration: README.md File

This guide will walk you through setting up an Amazon EKS Auto Mode cluster, deploying a sample application to see how it scales, and then cleaning up all the resources.

#### 1.1 AWS Console Steps

Follow these steps to create your EKS Auto Mode cluster and the necessary IAM roles.

1.  **Log in to the AWS Management Console**: Navigate to the **Elastic Kubernetes Service (EKS)** service.
2.  **Create an IAM Cluster Role**:
      * In the EKS console, click **Add cluster** -\> **Create**.
      * On the Configure cluster page, under **Cluster IAM role**, click the **Create recommended role** button. This will open a new tab in the IAM console.
      * The role creation wizard will pre-populate the necessary settings. Confirm that **EKS - Auto Cluster** is selected and click **Next**.
      * Review the permissions, click **Next**, give the role a name (e.g., `EKS-AutoMode-Cluster-Role`), and click **Create role**.
      * Go back to your EKS console tab and click the refresh button next to the role dropdown. Select the newly created role.
3.  **Create an IAM Node Role**:
      * Similarly, under **Auto Mode Compute**, find the **Node IAM role** field and click **Create recommended role**.
      * In the new IAM tab, the wizard will pre-populate the settings. Confirm that **EKS - Auto Node** is selected and click **Next**.
      * Review the permissions, click **Next**, give the role a name (e.g., `EKS-AutoMode-Node-Role`), and click **Create role**.
      * Return to your EKS console tab and select the new node role.
4.  **Create the EKS Auto Mode Cluster**:
      * Back on the EKS cluster creation page, select **Use EKS Auto Mode**.
      * Give your cluster a name and choose the desired Kubernetes version.
      * Click **Next** through the remaining screens, accepting the defaults.
      * Finally, click **Create**. The cluster status will show as "Creating" and will take a few minutes to become "Active."

#### 1.2 Install AWS CLI and `kubectl`

Before interacting with your new cluster, you need to install the necessary command-line tools.

1.  **Install AWS CLI**: Follow the official AWS documentation for your operating system to install the AWS CLI. You can find instructions for Windows, macOS, and Linux. After installation, configure it with your AWS credentials by running `aws configure`.
2.  **Install `kubectl`**: You can install `kubectl` from the official Kubernetes documentation or directly from Amazon EKS, which ensures a compatible version.
      * For example, on Linux:
        ```bash
        curl -o kubectl https://s3.us-west-2.amazonaws.com/amazon-eks/1.24/2023-01-26/bin/linux/amd64/kubectl
        chmod +x ./kubectl
        mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$HOME/bin:$PATH
        echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc
        ```
3.  **Configure `kubectl` to connect to your cluster**:
    ```bash
    aws eks update-kubeconfig --name <your-cluster-name> --region <your-aws-region>
    ```
    Replace `<your-cluster-name>` and `<your-aws-region>` with your cluster's name and region.

#### 1.3 Scale with a Sample Application

Let's deploy an application to test the scaling capabilities of EKS Auto Mode. We will use a simple NGINX deployment with a large number of replicas to force scaling.

1.  **Create a YAML file for the deployment and service**: Save the following content as `nginx-deployment.yaml`.
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: nginx-scale-test
      labels:
        app: nginx-scale-test
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: nginx-scale-test
      template:
        metadata:
          labels:
            app: nginx-scale-test
        spec:
          containers:
          - name: nginx
            image: nginx:latest
            ports:
            - containerPort: 80
            resources:
              requests:
                cpu: "500m"
    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: nginx-service
    spec:
      selector:
        app: nginx-scale-test
      ports:
        - protocol: TCP
          port: 80
          targetPort: 80
      type: LoadBalancer
    ```
2.  **Deploy the application**:
    ```bash
    kubectl apply -f nginx-deployment.yaml
    ```
3.  **Scale up the deployment to a large number of replicas**: This will trigger EKS Auto Mode (using Karpenter) to provision new nodes.
    ```bash
    kubectl scale deployment nginx-scale-test --replicas=50
    ```
4.  **Monitor the cluster**:
      * Run `kubectl get pods -w` to watch the pods being scheduled and started. You will notice that many pods are in a "Pending" state initially.
      * Run `kubectl get nodes` to see new nodes being provisioned by Karpenter to accommodate the new pods. It may take a few minutes for the new nodes to appear.
      * You can also check the EKS console under the "Compute" tab to see the new nodes being added to your cluster.
5.  **Scale down to demonstrate cost efficiency**:
      * To see the nodes removed, scale the deployment back down to a single replica.
    <!-- end list -->
    ```bash
    kubectl scale deployment nginx-scale-test --replicas=1
    ```
      * Wait for the extra pods to terminate, then run `kubectl get nodes -w` to watch the nodes being drained and terminated by Karpenter. This demonstrates how EKS Auto Mode is **cost-effective** by removing unused compute resources.

#### 1.4 Deleting Resources

After your demonstration, it's essential to clean up all the resources to avoid incurring unnecessary costs.

1.  **Delete the application deployment**: This will trigger the downscaling process.
    ```bash
    kubectl delete -f nginx-deployment.yaml
    ```
2.  **Delete the EKS cluster**:
      * Go to the **AWS EKS console**.
      * Select your cluster.
      * Click the **Delete** button in the top right corner.
      * Confirm the deletion by typing the cluster name and clicking **Delete**.
      * AWS will automatically delete the associated VPC, subnets, and other resources. You don't need to manually delete the IAM roles, but it is a good practice to clean them up from the IAM console after you confirm the cluster is fully deleted.

-----
