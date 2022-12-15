# Deploy quote-service as a serverless application

This allows the user to deploy an application without setting up anything on the server. The feature is available in most Cloud ecosystems (it actually does everything behind the scenes for setting up the server) and enables a developer to have the application running with little to no system level setup. In GCP there are several flavours of serverless deployments, but the most basic and the one that is presented here is 'Cloud Run'

For a quick setup we can use the 'Cloud Shell'. This comes included with any GCP project and is basically a Debian VM with several tools already installed. It does not show up in the user configurable VM Instances and it does not cost anything to run. To start a new session click the 'Activate Cloud Shell' in the top right corner of Google Cloud Console.

Once the shell sessions is started and console is dislayed in the bottom half of the screen, we can immediately start using it.

First, let's clone the application sources in a new folder:
```
mkdir github
cd github/ && git clone https://github.com/WebToLearn/fx-trading-app.git
```
Update the application to run on port 8080
```
cd fx-trading-app/App/quote-service/
sed -i 's/8220/8080/g' src/main/resources/application.properties
```

Make sure you have gcloud configured on the correct project
```
gcloud config get project
```

If not, set it to the correct one
```
gcloud config set project [REPLACE WITH OWN PROJECT_ID]
```

Deploy the application in Cloud Run
```
gcloud run deploy
```
- When you are prompted for the source code location, press Enter to deploy the current folder.
- When you are prompted for the service name, press Enter to accept the default name
- When you are prompted for region: select `europe-west3`
- When you are prompted to enable the Artifact Registry API, respond by pressing y
- You will be prompted to allow unauthenticated invocations: respond y 

Then wait a few moments until the deployment is complete. On success, the command line displays the service URL.

```
Done.
Service [quote-service] revision [quote-service-00002-wuv] has been deployed and is serving 100 percent of traffic.
Service URL: https://quote-service-hjizzxyvha-ey.a.run.app
```
