---
title: "Kubernetes Deployment Status ☸️"
date: 2023-06-19T01:27:59+05:30
draft: false
tags: ["kubernetes", "openshift", "python", "devops"]
---

## Overview 🔭

Kubernetes is a popular container orchestration platform that allows developers to manage and deploy containerized applications. 

One of the challenges of managing Kubernetes deployments is keeping track of the deployment status and ensuring that the latest code changes have been deployed successfully.


## Purpose 🚀

This package, `k8s-deployment-status` is available in `Python`.

It retrieves commit details from a GitHub API endpoint and deployment timestamp from Kubernetes API. 

It encapsulates methods to interact with the APIs, handle retries, and extract relevant data from the API response. 

Most of the data is memoized as well to avoid unnecessary API calls.


**Note**: As of now only public GitHub repos are supported.

## Installation 🔧

To install the package, run the following command:

```
pip install k8s-deployment-status
```

The package dependencies (`kubernetes` and `requests`) will be installed automatically.


## Usage 🏄‍♂️

### Environment Variables

Set necessary environment variables like so in your Kubernetes yaml file.

```yaml
env:
- name: GITHUB_OWNER
  value: "organisation/owner-name"
- name: GITHUB_REPO
  value: "repo-name"
- name: GITHUB_DEPLOYMENT_BRANCH
  value: "main"
- name: GITHUB_API_PAGE_SIZE
  value: "5"
- name: GITHUB_API_MAXIMUM_RETRIES
  value: "3"
```

`GITHUB_OWNER`

- _required:_ `true`
- _description:_ owner or organization name of the GitHub repository.


`GITHUB_REPO`

- _required:_ `true`
- _description:_ name of the GitHub repository.


`GITHUB_DEPLOYMENT_BRANCH`

- _default:_ `main`
- _required:_ `false`
- _description:_ branch used for deployments in the GitHub repository.


`GITHUB_API_PAGE_SIZE`

- _default:_ `5`
- _required:_ `false`
- _description:_ number of commits to fetch per request from the GitHub API.


`GITHUB_API_MAXIMUM_RETRIES`

- _default:_ `3`
- _required:_ `false`
- _description:_ maximum number of retries when making requests to the GitHub API.

### Import

Import the package and respective class in the respective module

```python
from k8s_deployment_status import DeploymentStatus

@app.route('/api/ros/v1/deployment_status', methods=['GET'])
def deployment_status():
    deployment_status_data = DeploymentStatus().get()
    return jsonify(deployment_status_data)
```

## Response Data 📊

```json
{
    "branch": "main",
    "commit_merged": "Thu, 15 Jun 2023 14:38:16 UTC",
    "commit_msg": "Add redis as required dependency",
    "commit_sha": "9c2ee47951a8d25c7aa1402998344c5470111eee",
    "deployed_at": "Thu, 15 Jun 2023 18:59:25 UTC"
}

```

## Links 🔗

__PyPI__: https://pypi.org/project/k8s-deployment-status/

__GitHub__: https://github.com/saltgen/k8s_deployment_status

If you like the idea, do 🌟 the repo on Github!