# 300 - Building Our Application

## 100 - Creating a RESTful API in N8N

Create a Webhook in N8N that will be triggered when a RESTful command is executed from an (external) application, such as Home Assistant.

Based on "The beginner's guide to webhooks for workflow automation" at https://blog.n8n.io/webhooks-for-workflow-automation/ 



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
