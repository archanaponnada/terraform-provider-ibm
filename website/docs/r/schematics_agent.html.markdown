---
layout: "ibm"
page_title: "IBM : ibm_schematics_agent"
description: |-
  Manages schematics_agent.
subcategory: "Schematics"
---

# ibm_schematics_agent

~> **Beta:** This resource is in Beta, and is subject to change.

Provides a resource for schematics_agent. This allows schematics_agent to be created, updated and deleted.

## Example Usage

```hcl
resource "ibm_schematics_agent" "schematics_agent_instance" {
  agent_infrastructure {
		infra_type = "ibm_kubernetes"
		cluster_id = "cluster_id"
		cluster_resource_group = "cluster_resource_group"
		cos_instance_name = "cos_instance_name"
		cos_bucket_name = "cos_bucket_name"
		cos_bucket_region = "cos_bucket_region"
  }
  agent_location = "us-south"
  agent_metadata {
		name = "purpose"
		value = ["git", "terraform", "ansible"]
  }
  description = "Create Agent"
  name = "MyDevAgent"
  resource_group = "Default"
  schematics_location = "us-south"
  version = "1.0.0-beta2"
}
```

## Argument Reference

Review the argument reference that you can specify for your resource.

* `agent_infrastructure` - (Required, List) The infrastructure parameters used by the agent.
Nested scheme for **agent_infrastructure**:
	* `cluster_id` - (Optional, String) The cluster ID where agent services will be running.
	* `cluster_resource_group` - (Optional, String) The resource group of the cluster (is it required?).
	* `cos_bucket_name` - (Optional, String) The COS bucket name used to store the logs.
	* `cos_bucket_region` - (Optional, String) The COS bucket region.
	* `cos_instance_name` - (Optional, String) The COS instance name to store the agent logs.
	* `infra_type` - (Optional, String) Type of target agent infrastructure.
	  * Constraints: Allowable values are: `ibm_kubernetes`, `ibm_openshift`, `ibm_satellite`.
* `agent_kpi` - (Optional, List) Schematics Agent key performance indicators.
Nested scheme for **agent_kpi**:
	* `application_indicators` - (Optional, List) Agent application key performance indicators.
	* `availability_indicator` - (Optional, String) Overall availability indicator reported by the agent.
	  * Constraints: Allowable values are: `available`, `unavailable`, `error`.
	* `infra_indicators` - (Optional, List) Agent infrastructure key performance indicators.
	* `lifecycle_indicator` - (Optional, String) Overall lifecycle indicator reported by the agents.
	  * Constraints: Allowable values are: `consistent`, `inconsistent`, `obselete`.
	* `percent_usage_indicator` - (Optional, String) Percentage usage of the agent resources.
* `agent_location` - (Required, String) The location where agent is deployed in the user environment.
* `agent_metadata` - (Optional, List) The metadata of an agent.
Nested scheme for **agent_metadata**:
	* `name` - (Optional, String) Name of the metadata.
	* `value` - (Optional, List) Value of the metadata name.
* `description` - (Optional, String) Agent description.
* `name` - (Required, String) The name of the agent (must be unique, for an account).
* `resource_group` - (Required, String) The resource-group name for the agent.  By default, agent will be registered in Default Resource Group.
* `schematics_location` - (Required, String) List of locations supported by IBM Cloud Schematics service.  While creating your workspace or action, choose the right region, since it cannot be changed.  Note, this does not limit the location of the IBM Cloud resources, provisioned using Schematics.
  * Constraints: Allowable values are: `us-south`, `us-east`, `eu-gb`, `eu-de`.
* `tags` - (Optional, List) Tags for the agent.
* `user_state` - (Optional, List) User defined status of the agent.
Nested scheme for **user_state**:
	* `set_at` - (Computed, String) When the User who set the state of the Object.
	* `set_by` - (Computed, String) Name of the User who set the state of the Object.
	* `state` - (Optional, String) User-defined states  * `enable`  Agent is enabled by the user.  * `disable` Agent is disbaled by the user.
	  * Constraints: Allowable values are: `enable`, `disable`.
* `version` - (Required, String) Agent version. Available Versions are 1.0.0-beta1, 1.0.0-beta2

## Attribute Reference

In addition to all argument references listed, you can access the following attribute references after your resource is created.

* `id` - The unique identifier of the schematics_agent.
* `agent_crn` - (String) The agent crn, obtained from the Schematics agent deployment configuration.
* `created_at` - (String) The agent creation date-time.
* `creation_by` - (String) The email address of an user who created the agent.
* `recent_deploy_job` - (List) Post-installations checks for Agent health.
Nested scheme for **recent_deploy_job**:
	* `agent_id` - (String) Id of the agent.
	* `agent_version` - (String) Agent version.
	* `is_redeployed` - (Boolean) True, when the same version of the agent was redeployed.
	* `job_id` - (String) Job Id.
	* `log_url` - (String) URL to the full agent deployment job logs.
	* `status_code` - (String) Final result of the agent deployment job.
	  * Constraints: Allowable values are: `pending`, `in-progress`, `success`, `failed`.
	* `status_message` - (String) The outcome of the agent deployment job, in a formatted log string.
	* `updated_at` - (String) The agent deploy job updation time.
	* `updated_by` - (String) Email address of user who ran the agent deploy job.
* `recent_health_job` - (List) Agent health check.
Nested scheme for **recent_health_job**:
	* `agent_id` - (String) Id of the agent.
	* `agent_version` - (String) Agent version.
	* `job_id` - (String) Job Id.
	* `log_url` - (String) URL to the full health-check job logs.
	* `status_code` - (String) Final result of the health-check job.
	  * Constraints: Allowable values are: `pending`, `in-progress`, `success`, `failed`.
	* `status_message` - (String) The outcome of the health-check job, in a formatted log string.
	* `updated_at` - (String) The agent health check job updation time.
	* `updated_by` - (String) Email address of user who ran the agent health check job.
* `recent_prs_job` - (List) Run a pre-requisite scanner for deploying agent.
Nested scheme for **recent_prs_job**:
	* `agent_id` - (String) Id of the agent.
	* `agent_version` - (String) Agent version.
	* `job_id` - (String) Job Id.
	* `log_url` - (String) URL to the full pre-requisite scanner job logs.
	* `status_code` - (String) Final result of the pre-requisite scanner job.
	  * Constraints: Allowable values are: `pending`, `in-progress`, `success`, `failed`.
	* `status_message` - (String) The outcome of the pre-requisite scanner job, in a formatted log string.
	* `updated_at` - (String) The agent prs job updation time.
	* `updated_by` - (String) Email address of user who ran the agent prs job.
* `system_state` - (List) Computed state of the agent.
Nested scheme for **system_state**:
	* `status_code` - (String) Agent Status.
	  * Constraints: Allowable values are: `error`, `normal`, `in_progress`, `pending`, `draft`.
	* `status_message` - (String) The agent status message.
* `updated_at` - (String) The agent registration updation time.
* `updated_by` - (String) Email address of user who updated the agent registration.

## Import

You can import the `ibm_schematics_agent` resource by using `id`. The agent resource id.

# Syntax
```
$ terraform import ibm_schematics_agent.schematics_agent <id>
```
