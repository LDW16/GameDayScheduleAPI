# AWS ECR & ECS Troubleshooting Guide  

## 1. Navigate to the Amazon ECR Console  
- Open the [Amazon ECR console](https://console.aws.amazon.com/ecr/)  

## 2. Verify the Existence of the `sports-api` Repository  
- Check if the repository **`sports-api`** exists in your ECR  
- If it **does not** exist, create a new repository named **`sports-api`**  

## 3. Check the Image Tag in the Repository  
- Look for the **`sports-api-latest`** tag in the **`sports-api`** repository  
- If the tag is **missing**, ensure the correct image is pushed to the repository with the **`sports-api-latest`** tag  

## 4. Permission Issues  
- If you **do not** have permissions to perform the above actions, contact your **AWS Administrator**  

## 5. Verify ECS Task Execution Role Permissions  
1. Go to the [IAM console](https://console.aws.amazon.com/iam/)  
2. Find the **task execution role** used by your ECS task  
3. Ensure it has the necessary permissions to pull images from **ECR**  
4. If needed, attach the following policy to the role:  

    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "ecr:GetAuthorizationToken",
                    "ecr:BatchCheckLayerAvailability",
                    "ecr:GetDownloadUrlForLayer",
                    "ecr:BatchGetImage"
                ],
                "Resource": "arn:aws:ecr:us-east-1:137068223119:repository/sports-api"
            }
        ]
    }
    ```

## 6. Update the ECS Task Definition  
1. Open the [ECS console](https://console.aws.amazon.com/ecs/)  
2. Navigate to **Task Definitions**  
3. Locate the **task definition** used by the failing task  
4. Click **Create new revision**  
5. Ensure the **image URI** is set correctly:  
    ```
    <youraccountid>.dkr.ecr.us-east-1.amazonaws.com/sports-api
    ```
6. Click **Update** to save the new revision  

## 7. Update the ECS Service  
1. In the [ECS console](https://console.aws.amazon.com/ecs/), go to **Clusters**  
2. Select the cluster **`sports-api-cluster`**  
3. Click on the service running the failing task  
4. Click **Update**  
5. Select the new **task definition revision** created in Step 6  
6. Click **Deploy** to apply the update  

## 8. Monitor the Service  
1. In the **ECS console**, go to the **`sports-api-cluster`**  
2. Monitor the **Tasks** tab to check for new tasks being created  
3. Verify that new tasks are able to **pull the image** and start successfully  
4. If tasks continue to fail, check ECS task logs and **CloudWatch** for error messages  

---

**Note:** If issues persist, ensure your AWS credentials are correct and that the ECS service has the appropriate IAM permissions.  
