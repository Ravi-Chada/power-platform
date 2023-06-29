---
title: "Overview of pipelines in Power Platform"
description: "Overview of pipelines in Power Platform and frequently asked questions."
author: caburk
ms.subservice: alm
ms.author: matp
ms.custom: ""
ms.date: 06/20/2023
ms.reviewer: "matp"
ms.topic: "overview"
---
# Overview of pipelines in Power Platform

Pipelines in Power Platform aim to democratize application lifecycle management (ALM) for Power Platform and Dynamics 365 customers by bringing ALM automation and continuous integration and continuous delivery (CI/CD) capabilities into the service in a manner that's more approachable for all makers, admins, and developers.

:::image type="content" source="media/deployment-pipelines.png" alt-text="Example of the deployment Pipelines feature":::

Pipelines significantly reduce the effort and domain knowledge previously required to realize the ROI from adopting healthy, automated ALM processes within your team or organization.

- Admins easily configure automated deployment pipelines in minutes rather than days or weeks.
- Makers have an intuitive user experience for easily deploying their solutions.
- Professional developers can (optionally) [extend pipelines](extend-pipelines.md) and run them using the Power Platform command line interface (CLI).

## Admins centrally manage and govern pipelines

Pipelines enable admins to centrally govern citizen-led and pro-dev-led projects at scale with less effort. Admins set up the appropriate safeguards that govern and facilitate solution development, testing, and delivery across the organization. Other admin benefits include:

- Lower total cost of ownership:
  - Pipelines significantly improve maker, developer, and admin productivity. Pipelines enable your business solutions to come to market faster, with higher quality, through a safe and governed process.
  - Minimal effort to implement custom-tailored change management processes across your organization or team.

- Save time and money:
  - The system handles the heavy lifting and ongoing maintenance so you don't have to.

- Scale ALM at your own pace:
  - Regardless of where you're at in your ALM journey, you can extend pipelines to accommodate your evolving business needs. We aim for this upward transition to be as seamless and effortless as possible. More information: [Microsoft Power Platform CLI](../developer/cli/introduction.md)
- Achieve compliance, safety, monitoring, and automation goals with:
  - Customizations and audit logs saved automatically and are easily accessible.
  - Out-of-the-box analytics provides better visibility within a central location.
  - The ability to view out-of-the-box Power BI reports within the pipelines app or create your own. More information: [Reporting overview for model-driven apps](/power-apps/maker/model-driven-apps/reporting-overview)
  - Custom tailor pipelines to the needs of your organization with [pipelines extensibility](extend-pipelines.md) and Power Automate. 

## Makers run preconfigured pipelines

Once pipelines are in place, makers can initiate in-product deployments with a few clicks. They do so directly within their development environments. Other benefits to makers include:

- No prior knowledge of ALM processes or systems required. Citizen developers often view pipelines as a guided change management process.
- Solution deployments are prevalidated against the target environment to prevent mistakes and improve success rates. For example, missing dependencies and other issues are detected before deployment and makers are immediately guided to take the appropriate action.
- Connections and environment variables are provided upfront and validated before the deployment begins.
  - This helps ensure applications and automation are deployed without needing manual post-processing steps, and are connected to the appropriate data sources within each environment.
  - Admins can even preconfigure certain connections that will be used.

## Developers can use and extend pipelines

Professional developers are more productive with pipelines now handling the complex background operations. Developers can tell the system what they want to accomplish instead of executing the various underlying tasks necessary to accomplish the same goal. Using the Power Platform CLI, developers can:

- List pipelines to view pertinent details such as which stages and environments are ready to deploy their solutions to.
- Deploy a solution with a single command:
  - With pipelines, developers simply provide the required parameters and the system orchestrates all the end-to-end deployment operations in compliance with the organizational policies.
  - No need to connect to multiple environments, export solutions, download solution files, manually create connections and populate deployment settings files, import solutions, or handle various other tasks that were required previously.

Additionally, developers can [extend pipelines](extend-pipelines.md) and integrate with other CI/CD tools.

## Frequently asked questions

### What do pipelines deploy?

Pipelines deploy solutions as well as configuration for the target environment such as connections, connection references, and environment variables. Any Power Platform customization contained in your solution can be deployed using pipelines. Pipelines, or solutions in general, don't contain data stored within Dataverse tables.

   > [!IMPORTANT]
   >
   > Power BI Dashboards (preview) and Power BI Datasets (preview) are not currently supported in pipelines. 
   >

### Does pipelines automatically store solution backups?

Yes. Both managed and unmanaged solutions are automatically exported and stored in the pipelines host for every deployment.

### Can customization bypass a deployment stage such as QA?

No. Solutions are exported as soon as a deployment request is submitted (when the maker selects **Deploy** from within their development environment), and the same solution artifact will be deployed. Similarly, the system doesn't re-export a solution for deployments to subsequent stages in a pipeline. The same solution artifact must pass through pipeline stages in sequential order. The system also prevents any tampering or modification to the exported solution artifact. This ensures customization can't bypass QA environments or your approval processes.

### Are standalone licenses required to use pipelines?

- Both source and target environments must be enabled as Managed Environments. Managed Environments isn't required for the pipelines host. 
- Standalone licenses aren't required to enable Managed Environments for developer and trial type environments.

A common setup example:

| Environment purpose | Environment type |  Standalone license required |
|--------------|-----|-----------|
| Host | Production | No |
| Development | Developer | No |
| QA |  Developer | No |
| Production |  Production | Yes |

### Can I configure approvals for deployments?

Yes. You can use the pipelines extensibility feature with Power Automate and other approval systems. Notice that to run pipelines, you currently need permission to import solutions to the target environment.

### Can pipelines deploy to a different tenant?

No. We recommend using Azure DevOps or GitHub for this scenario. 

### What should I do if my development or target environment is reset or deleted?

You should delete the environment record and update the pipeline configuration when needed. If an environment is reset, you re-create the environment record then associate it with your pipeline. 

### Can I use pipelines in the default environment?

Yes. However, using the default environment as the pipelines host isn't recommended for all customers. 

### Can I deploy using my own service principal?

Not currently. 

### Can pipelines be used with Azure DevOps, GitHub, or the ALM Accelerator?

Yes, together these tools are powerful while keeping maker experiences simple. More information: [extend pipelines](extend-pipelines.md)

### Can I roll back to a previous version?

Not currently. The same is true when manually importing solutions.

### Can I set retention policicies for pipelines data?
Yes. You can configure bulk delete jobs in the Dataverse pipelines host to delete data on a defined schedule. 

### Can I specify advanced solution import behaviors such as update versus upgrade?

Not currently. Pipelines default import behavior is _Upgrade_ with _Maintain customizations_.

### Can an environment be associated with multiple hosts?

No. However, one environment can be linked to multiple pipelines within the same host. In order to associate an environment with a different host, add it to a pipeline in the new host. Then delete the environment record from the original host and verify everything works as expected.

### Can I customize or extend the first-party deployment pipeline app and tables?

Not currently. However, intentional extension hooks are available to customize pipelines logic. More information: [extend pipelines](extend-pipelines.md).

### Where can I view and run pipelines?

Currently within any development environments associated with a pipeline. Pipelines can't be viewed or run from within target environments. Notice you can also retrieve and run pipelines from the Power Platform CLI.

### Can I deploy across regions?

Not currently. The host and all environments associated with pipelines in a host must be located within the same geographic location (as specified when creating environments). For example, a pipeline can't deploy from Germany to Canada. And a host in Germany shouldn't manage environments in Canada. Instead, separate hosts should be used for Germany and Canada.

### Can I deploy the same solution using different pipelines?

Yes, this is possible, although we recommend starting with the same pipeline for a given solution. This helps avoid confusion and inadvertent mistakes. Pipeline run information is displayed in the context of one pipeline and one solution (within the solution experience). Therefore other pipelines may not show the latest deployed solution version or other important run information associated with different pipelines. Notice that the Deployment Pipeline Configuration app shows run information across all pipelines and all solutions for the current host.

### Can the host environment also be used as a development or target environment?

While possible, this isn't typically recommended; especially for development environments that may be deleted or reset. 

### How can I view what changed between different versions?

Within the target environment, you can see layers of deployed objects as well as what changed between layers. Additionally, you can see XML diffs between layers for model-driven apps, site maps, and forms. Pipelines can also be extended to integrate with GitHub and other source control systems to compare granular diffs. 

### Should my host environment be the same as where I installed the COE toolkit?

This is a valid configuration and should be evaluated based on the needs and policies within your organization.

### Can I deploy unmanaged solutions?

No. We recommend that you always deploy managed solutions to non-development environments. Notice unmanaged solutions are automatically exported and stored in the pipelines host so you can download and import them to other development environments or put them in source control. 

### Can I deploy multiple solutions at once?

Not currently. You'll need to submit a different deployment for each solution. However, the same pipeline can be used for multiple solutions.

### Do pipelines publish unmanaged customizations before exporting the solution?

Not currently. We recommend you publish individual objects as they're saved. Note that only certain solution objects require publishing.

### Can I use pipelines for multi-developer teams working in isolated development environments?

The current implementation uses a single development environment for a given solution.

### How are pipelines different from the ALM Accelerator?

Both offer many valuable capabilities and the owning teams work together closely in developing the pipelines and broader ALM vision for Power Platform. Pipelines are more simplistic in nature and can be set up and managed with less effort. Access to other products and technologies isn't required as everything is managed in-house. The ALM Accelerator, on the other hand, is sometimes a better fit for more advanced ALM scenarios.

While there are many additional functional differences, the fundamental difference is that pipelines are an official Microsoft Power Platform product feature—meaning it's designed, architected, engineered, tested, maintained, and supported by Microsoft product engineering. Pipelines are built into the product and can be accessed within native product experiences.

### When should I use pipelines versus another tool?

We encourage customers to use pipelines for core deployment functionality, and when needed, extend pipelines to integrate with other CI/CD tools. When used together, the workloads required within CI/CD tools often become less complicated and costly to maintain. 

### Can I use impersonation to deploy on behalf of another user?
This is not supported.

## Next steps

[Set up pipelines](set-up-pipelines.md)
[Extend pipelines](extend-pipelines.md)

[!INCLUDE[footer-include](../includes/footer-banner.md)]