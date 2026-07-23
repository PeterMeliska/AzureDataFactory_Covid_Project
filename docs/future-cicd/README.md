## Future CI/CD Implementation

As a separate hands-on exercise, I explored two CI/CD approaches for deploying Azure Data Factory across **Development, Test and Production** environments.

This implementation is not currently part of the COVID Reporting project. It represents a potential future approach for controlled and repeatable production deployment.

### Option 1 – ADF Publish
Developers work with feature branches and merge approved changes into the collaboration branch. Publishing from the development Data Factory generates ARM templates in the `adf_publish` branch.

![CI/CD using ADF Publish](CICD-Option1.png)

The generated ARM template is used as the deployment artifact by an Azure DevOps Release Pipeline. Changes are first deployed to the **Test** environment and can then be promoted to **Production** after validation or approval.

![CI/CD using ADF Publish](CICD-Option1PL.png)

This option is simple and uses the native ADF publishing process, but ARM template generation depends on a developer manually selecting **Publish** in ADF Studio.

### Option 2 – Automated Build Pipeline

In the second approach, merging changes into the collaboration branch starts an automated Build Pipeline. The build validates the ADF resources and generates the ARM deployment artifacts without requiring a manual publish action.

![CI/CD using ADF Publish](CICD-Option2.png)

The generated artifact is passed to the Release Pipeline and promoted through **Development, Test and Production** stages. Environment-specific parameters and approvals can be applied before each deployment.

![CI/CD using ADF Publish](CICD-Option2PL.png)

This approach provides greater automation, repeatability and consistency, making it more suitable for a mature production deployment process.

### Comparison

| Approach | ARM template generation | Main advantage |
| --- | --- | --- |
| ADF Publish | Manual publish from ADF Studio | Simpler initial setup |
| Automated Build Pipeline | Generated automatically during the build | Repeatable and scalable deployment |

The exercise helped me understand Git-based ADF development, ARM template generation, deployment artifacts, environment-specific configuration and controlled promotion across Azure environments.
