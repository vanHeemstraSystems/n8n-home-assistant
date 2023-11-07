# 300 - Testing

Go to developer tools and test it out.

First, restart the server (**Configuration -> Server Controls -> RESTART**) to apply the new changes:

1. Go to Home Assistant’s **Developer Tools -> Services** screen
2. Select "rest_command.trigger_n8n" from the Service menu
3. Enter the following in the Service Data field to trigger your n8n workflow:
   {"bar":"some information"}
4. Select the CALL SERVICE button

You must replace ```some information``` with some information you want to make use of in your n8n workflow(s).

And that’s it!

You can now start triggering n8n workflows from Home Assistant.

In addition, see https://voicemonkey.io/integrations/home-assistant

