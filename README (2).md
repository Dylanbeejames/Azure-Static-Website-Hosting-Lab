# Azure Static Website Hosting Lab

**Author:** Dylan  
**Role:** Cloud Security Specialist  
**Video Walkthrough:** [▶ Watch on Loom](https://www.loom.com/share/987d874d60ad4f8a8f020ad0a57306ce)  
**Live Demo:** [stlab01dylanbryson.z13.web.core.windows.net](https://stlab01dylanbryson.z13.web.core.windows.net/)

---

## Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Technologies Used](#technologies-used)
- [Phase 1 — Create Resource Group](#phase-1--create-resource-group)
- [Phase 2 — Create Storage Account](#phase-2--create-storage-account)
- [Phase 3 — Enable Static Website Hosting](#phase-3--enable-static-website-hosting)
- [Phase 4 — Build and Upload the Website](#phase-4--build-and-upload-the-website)
- [Phase 5 — Validate Deployment](#phase-5--validate-deployment)
- [Phase 6 — Cleanup](#phase-6--cleanup)
- [Key Takeaways](#key-takeaways)
- [Next Steps](#next-steps)

---

## Overview

This lab demonstrates how to host a **serverless static website** using **Azure Blob Storage**. Rather than provisioning or managing any virtual machines or web servers, Azure's built-in static website hosting feature is used to publish a live site directly to the internet via a public endpoint.

This pattern is ideal for portfolios, documentation sites, landing pages, and any content that doesn't require server-side processing.

---

## Architecture

```
User → Azure Static Website Endpoint → Storage Account ($web container) → index.html
```

No compute resources are involved. Azure handles routing all HTTP requests to the files stored in the `$web` container, making this a fully managed, serverless delivery model.

---

## Technologies Used

| Technology | Purpose |
|------------|---------|
| Azure Resource Group | Container for all lab resources |
| Azure Storage Account | Hosts the static website backend |
| Azure Blob Storage (`$web`) | Stores and serves the website files |
| Static Website Hosting | Azure-native feature for public file serving |
| HTML | Website content |

---

## Phase 1 — Create Resource Group

| Setting | Value |
|---------|-------|
| Name | `rg-lab01-dylanbryson1` |
| Region | East US |

The resource group acts as the logical container for all resources in this lab, making management and cleanup straightforward.

---

## Phase 2 — Create Storage Account

| Setting | Value |
|---------|-------|
| Name | `stlab01dylanbryson1` |
| Performance | Standard |
| Redundancy | Locally Redundant Storage (LRS) |

> **Note:** LRS replicates data three times within a single datacenter region — sufficient for a lab or low-criticality static site. For production workloads, consider **Zone-Redundant Storage (ZRS)** or **Geo-Redundant Storage (GRS)** for higher availability.

---

## Phase 3 — Enable Static Website Hosting

1. Navigate to the Storage Account in the Azure Portal
2. Under **Data Management**, select **Static website**
3. Toggle the feature to **Enabled**
4. Set the **Index document name** to `index.html`
5. Save — Azure generates a public endpoint URL automatically

The endpoint follows this format:

```
https://<storage-account-name>.z13.web.core.windows.net/
```

---

## Phase 4 — Build and Upload the Website

1. Create an `index.html` file with your site content
2. In the Azure Portal, navigate to **Containers → $web**
3. Upload `index.html` to the `$web` container

> The `$web` container is automatically created by Azure when static website hosting is enabled. All files uploaded here are publicly accessible via the endpoint.

---

## Phase 5 — Validate Deployment

Open a browser and navigate to the generated public endpoint:

```
https://stlab01dylanbryson.z13.web.core.windows.net/
```

A successful page load confirms the static website is live and Azure is correctly serving content from the `$web` container.

---

## Phase 6 — Cleanup

To remove all resources and avoid storage charges:

1. Open the **Azure Portal**
2. Navigate to **Resource Groups**
3. Select `rg-lab01-dylanbryson1`
4. Click **Delete Resource Group** and confirm

> ⚠️ Deleting the resource group removes the storage account and all hosted content permanently.

---

## Key Takeaways

- ✅ Hosted a static website in Azure without provisioning any servers
- ✅ Understood how Blob Storage functions as a web hosting backend
- ✅ Practiced deploying and validating cloud resources end-to-end
- ✅ Gained experience with public endpoints and Azure storage redundancy options

---

## Next Steps

| Enhancement | Description |
|-------------|-------------|
| **Azure CDN** | Front the storage endpoint with a CDN for global performance and custom domain support |
| **Custom Domain + HTTPS** | Map a custom domain and enforce HTTPS via Azure CDN or Static Web Apps |
| **Azure Static Web Apps** | Migrate for CI/CD integration with GitHub Actions |
| **Lifecycle Management Policy** | Add blob lifecycle rules to auto-manage old or unused files |
| **Logging & Monitoring** | Enable Azure Monitor and Storage diagnostics to track traffic and errors |

---

*© Dylan — Cloud Security Specialist*
