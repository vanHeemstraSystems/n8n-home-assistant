# 200 - Trigger N8N With The RESTful Command

Based on "rest_command" at https://www.home-assistant.io/integrations/rest_command/

In Home Assistant you can make API calls using the REST command.

Simply add the following to Home Assistant’s **configuration.yaml** file:

```
# Self-hosted N8N Routine API call
rest_command:
  trigger_n8n:
    url: https://<N8N_HOST>:<N8N_PORT>/<N8N_PATH>/api/v<version-number>/workflows?<workflow_id>
    method: POST
    headers:
      accept: "application/json"
      X-N8N-API-KEY: <your-api-key>
    verify_ssl: true
    content_type:  'application/json; charset=utf-8'
    payload: '{"foo":"{{bar}}"}'

# End of N8N Routine API call
```

OR

```
# Cloud-hosted N8N Routine API call
rest_command:
  trigger_n8n:
    url: https://<your-cloud-instance>/api/v<version-number>/workflows?<workflow_id>
    method: POST
    headers:
      accept: "application/json"
      X-N8N-API-KEY: <your-api-key>
    verify_ssl: true
    content_type:  'application/json; charset=utf-8'
    payload: '{"foo":"{{bar}}"}'

# End of N8N Routine API call
```

In the code above you should replace ```<your-api-key>``` with your own API token found in the N8N console (make sure you keep it secret!). See https://docs.n8n.io/api/authentication/

Even better, keep your tokens in the a ```secrets.yaml``` file to ensure they don’t accidently get leaked by way of a public Github post etc.
