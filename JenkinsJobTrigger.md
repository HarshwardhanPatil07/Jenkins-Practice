![alt text](Trigger.png)

1. Get Gitlab Plugin and create token in gitlab under access token 

2. Jenkins will talk with the Gitlab for build

3. in pipeline general settings after adding token in system settings check the box of build when a change is pushed to gitlab under build triggers

4. Now go to Gitlab and project settings there under Integrations find Jenkins Enable the integration and Push. Enter details of jenkins server url. under project name same as pipeline name.

5. For Multibranch Pipeline you need different plugin (Multibranch scan webhook Trigger) also you need to select scan by webhook under build configuration;  form the webhooks url by trigger token name; The url in gitlab accepts call from jenkins;
