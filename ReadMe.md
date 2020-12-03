# Hackathon Starter Ansible Playbook

This Ansible playbook deploy the Hackathon Starter, A boilerplate for Node.js web applications to IKS cluster using ansible. 
Github URL: https://github.com/sahat/hackathon-starter/blob/master/README.md

## Steps to run with IBM Cloud Schematics. 

1. Create an `Action` with the following payload. 

```
{
  "name": "Hackathon_Starter_Action",
  "description": "This Action will deploy boiler plate code for Hackathon Starter",
  "location": "us-east",
  "resource_group": "Default",
   "source": {
       "source_type" : "git",
       "git" : {
            "git_repo_url": "https://github.com/rvsingh011/AnsiblePlaybook"
       }
  },
  "command_parameter": "ansible_playbook.yaml",
  "tags": [
    "string"
  ],
  "inputs": [
    {
      "name": "cluster_id",
      "value": <You-Cluster-ID>,
      "metadata": {
        "type": "string",
        "default_value": <Your-Default-Cluster-ID>,
      }
    }
  ],
  "source_type": "GitHub" 
}
```

2. Create Job with the above action. 
```
{
  "command_object": "action",
  "command_object_id": <Action-ID>,
  "command_name": "ansible_playbook_run",
  "command_parameter": "ansible_playbook.yaml"
}
```

3. Once the job complete browse to your cluster public ip, Welcome screen should be up and running. 

![](./welcome_screen.png)


## Debug 

For debugging purpose create action with verbose settings.

```
"inputs": [...],
"settings":[
      {
      "name": "verbose",
      "value": "4",
       "metadata": {
        "type": "string",
        "default_value": "0",
        "secure": false,
        "immutable": false,
        "hidden": false
      }
      }
  ],
  "tags": [
    "string"
  ]
  ```

