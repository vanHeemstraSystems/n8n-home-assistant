# 300 - Building Our Application

## 100 - Trigger N8N With The RESTful Command

In Home Assistant you can make API calls using the REST command.

Simply add the following to Home Assistant’s **configuration.yaml** file:

```
# N8N Routine API call
rest_command:
trigger_n8n:
    url: https://api-v2.voicemonkey.io/trigger
    method: POST
    verify_ssl: true
    content_type:  'application/json; charset=utf-8'
    payload: '{"token":"API_TOKEN","device":"{{deviceId}}"}'

# End of N8N Routine API call
```

In the code above you should replace API_TOKEN with your own API token found in the N8N console (make sure you keep it secret!). See https://docs.n8n.io/api/authentication/

Even better, keep your tokens in the a ```secrets.yaml``` file to ensure they don’t accidently get leaked by way of a public Github post etc.

