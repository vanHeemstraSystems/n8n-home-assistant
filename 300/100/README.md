# 100 - Creating a RESTful API in N8N

**TIP**: Use your API Key to control n8n programmatically using the n8n API. But if you only want to trigger workflows, consider using the webhook node instead.

Based on "API Authentication" at https://docs.n8n.io/api/authentication/

n8n uses API keys to authenticate API calls.

## 100 - Create an API key

1. Log in to n8n ([cloud for wvanheemstra](https://wvanheemstra.app.n8n.cloud)).
2. Go to **Settings > n8n API**.
3. Select **Create an API key**.

## 200 - Delete an API key

1. Log in to n8n ([cloud for wvanheemstra](https://wvanheemstra.app.n8n.cloud)).
2. Go to **Settings > n8n API**.
3. Select **Delete** next to the key you want to delete.

## 300 - Call the API using your key

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

For ```<version-number>``` choose ```v.1```.

## 400 - Call the WebHook using your key

If instead of an API, you have configured a WebHook in n8n, send the API key in your WebHook call as a header named **X-N8N-API-KEY**.

For example, say you want to the ```activity``` webhook. Your curl request will look like this:

```
# For a self-hosted n8n instance
curl -X 'POST' \
  '<N8N_HOST>:<N8N_PORT>/<N8N_PATH>/webhook/v<version-number>/activities' \
  -H 'accept: application/json' \
  -H 'X-N8N-API-KEY: <your-api-key>'

# For n8n Cloud
curl -X 'POST' \
  '<your-cloud-instance>/webhook/v<version-number>/activities' \
  -H 'accept: application/json' \
  -H 'X-N8N-API-KEY: <your-api-key>'
```
For a test webhook, use ```webhook-test``` instead of ```webhook```.
For ```<version-number>``` choose ```v.1```.

MORE ...

