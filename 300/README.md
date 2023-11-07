# 300 - Building Our Application

## 100 - Creating a RESTful API in N8N

**TIP**: Use your API Key to control n8n programmatically using the n8n API. But if you only want to trigger workflows, consider using the webhook node instead.

Based on "API Authentication" at https://docs.n8n.io/api/authentication/

n8n uses API keys to authenticate API calls.

### 100 - Create an API key

1. Log in to n8n ([cloud for wvanheemstra](https://wvanheemstra.app.n8n.cloud)).
2. Go to **Settings > n8n API**.
3. Select **Create an API key**.

### 200 - Delete an API key

1. Log in to n8n ([cloud for wvanheemstra](https://wvanheemstra.app.n8n.cloud)).
2. Go to **Settings > n8n API**.
3. Select **Delete** next to the key you want to delete.

### 300 - Call the API using your key

Send the API key in your API call as a header named **X-N8N-API-KEY**.

For example, say you want to get all active workflows. Your curl request will look like this:

```
# For a self-hosted n8n instance
curl -X 'GET' \
  '<N8N_HOST>:<N8N_PORT>/<N8N_PATH>/api/v<version-number>/workflows?active=true' \
  -H 'accept: application/json' \
  -H 'X-N8N-API-KEY: <your-api-key>'

# For n8n Cloud
curl -X 'GET' \
  '<your-cloud-instance>/api/v<version-number>/workflows?active=true' \
  -H 'accept: application/json' \
  -H 'X-N8N-API-KEY: <your-api-key>'
```

MORE ...


## 200 - Trigger N8N With The RESTful Command

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

## 300 - Testing

Go to developer tools and test it out.

First, restart the server (**Configuration -> Server Controls -> RESTART**) to apply the new changes:

1. Go to Home Assistant’s **Developer Tools -> Services** screen
2. Select "rest_command.trigger_n8n" from the Service menu
3. Enter the following in the Service Data field to trigger your n8n workflow:
   {"bar":"some information"}
4. Select the CALL SERVICE button

You must replace ```some information``` with the some information you want to make use of in your n8n workflow(s).

And that’s it!

You can now start triggering n8n workflows from Home Assistant.

In addition, see https://voicemonkey.io/integrations/home-assistant
