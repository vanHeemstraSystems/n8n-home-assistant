# 300 - Building Our Application

## 100 - Creating a RESTful API in N8N

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

In Home Assistant you can make API calls using the REST command.

Simply add the following to Home Assistant’s **configuration.yaml** file:

```
# N8N Routine API call
rest_command:
  trigger_n8n:
    url: https://~~api-v2.voicemonkey.io~~/trigger  # REPLACE WITH N8N URL
    method: POST
    verify_ssl: true
    content_type:  'application/json; charset=utf-8'
    payload: '{"token":"API_TOKEN","device":"{{deviceId}}"}'

# End of N8N Routine API call
```

In the code above you should replace API_TOKEN with your own API token found in the N8N console (make sure you keep it secret!). See https://docs.n8n.io/api/authentication/

Even better, keep your tokens in the a ```secrets.yaml``` file to ensure they don’t accidently get leaked by way of a public Github post etc.

## 300 - Testing

Go to developer tools and test it out.

First, restart the server (**Configuration -> Server Controls -> RESTART**) to apply the new changes:

1. Go to Home Assistant’s **Developer Tools -> Services** screen
2. Select "rest_command.trigger_n8n" from the Service menu
3. Enter the following in the Service Data field to trigger your n8n trigger device:
   {"deviceId":"N8N_ID"}
4. Select the CALL SERVICE button

You must replace N8N_ID with the ID of your N8N trigger device found in the Devices manager section of the console.

And that’s it!

You can now start triggering N8N Routines from Home Assistant.

More, see https://voicemonkey.io/integrations/home-assistant
