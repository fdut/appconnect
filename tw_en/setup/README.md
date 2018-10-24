# Prepare your environment

## Create a account on IBM Cloud public

1.  Visit [https://console.bluemix.net/](https://console.bluemix.net/) in your web browser.

1.  Press the `Create a free account` button:

    ![](./img/createaccount.png)

1.  Complete the form and press the `Create Account` button.

1.  You will receive an email asking you to confirm your email address. Check your email and click the `Confirm Account` Confirm Account link..

1.  Once confirmed, you will be asked to Log in. Click on the `Log in` link and follow the instructions to enter your credentials and log in. Une fois confirmé, vous serez invité à vous connecter.

    ![](./img/confirmed.png)

## Set up your IBM Cloud Organization

1. You will be prompted to **Create organization**. Enter an organization name (notice that there are suggestions for you). Also select an appropriate region. Then press the`Create` button.

   ![](./img/create-org.png)

1. Next you will be prompted to **Create space**. Name your space `dev` and click on the `Create` button.

1. Finally, you will see the Summary page where you can review your entries. Click the `I'm Ready` button.

   ![](./img/im-ready.png)

## Browse the Bluemix Catalog and Attach the AppConnect Service

1.  In the top right-hand corner of the screen, select the `Catalog` button to browse the list of available Bluemix offerings.

    ![](./img/bmx-catalog.png)

1.  Once in the catalog, you can search for the API Connect service by entering in `API Connect` in the search box next to the magnifying glass icon. Click on the `API Connect` Icon to install a new instance of API Connect into your Bluemix space.

    ![](./img/apic-service.png)

1.  You can read through some of the details about the service. Select the Lite pricing plan and click on the `Create button.

    ![](./img/planlite.png)

1.  Once the API Connect service is attached to your account, you will be automatically launched into the API Drafts screen.

## Download IBM App Connect Enterprise

https://developer.ibm.com/integration/docs/app-connect-enterprise/get-started/

## Configuring an integration server by using CLI

- Create a node using:

**mqsicreatebroker TESTNODE**

```
BIP8071I: Successful command completion.
```

- Verify the node using:

**mqsicvp TESTNODE**

```
BIP8873I: Starting the component verification for component 'TESTNODE'.
BIP8876I: Starting the environment verification for component 'TESTNODE'.
BIP8894I: Verification passed for 'Registry'.
BIP8894I: Verification passed for 'MQSI_REGISTRY'.
BIP8894I: Verification passed for 'Java Version - 1.8.0 IBM Linux build 8.0.5.15 - pxa6480sr5fp15-20180502_01(SR5 FP15)
BIP8894I: Verification passed for 'MQSI_FILEPATH'.
BIP8878I: The environment verification for component 'TESTNODE' has finished successfully.
BIP8882I: Starting the WebSphere MQ verification for component 'TESTNODE'.
BIP8294I: ODBC environment verification was skipped because the ODBCINI environment variable is not set.
BIP8874I: The component verification for 'TESTNODE' has finished successfully.
BIP8071I: Successful command completion.
```

- Start the node using:

**mqsistart TESTNODE**

```
BIP8096I: Successful command initiation, check the system log to ensure that the component started without problem and that it continues to run without problem.
```

- List all nodes using:

**mqsilist**

```
BIP1325I: Integration node 'TESTNODE' with administration URI 'http://localhost:4470' is running.
BIP8071I: Successful command completion.
```

- Create a server on the node using:

**mqsicreateexecutiongroup TESTNODE -e TESTSERVER -w 99**

```
BIP1124I: Creating integration server 'TESTSERVER' on integration node 'TESTNODE'...
BIP1117I: The integration server was created successfully.

The integration node has initialized the integration server.
BIP8071I: Successful command completion.
```

- List the server status using:

**mqsilist TESTNODE**

```
BIP1286I: Integration server 'default' on integration node 'TESTNODE' is running.
BIP8071I: Successful command completion.
```

## Import Callable flow WriteToFile

-> IBM AppConnect > Manage Callable Flow > Connect Callable flow

Clic on button 'Download the Configuration' and Save file

Copy the saved file (agentx.json) in the Directory C:\ProgramData\IBM\MQSI\config\TESTNODE\TESTSERVER\iibswitch\agentx

And Clic on button 'Test your agent'

Set Root Directory : MQSI_FILENODES_ROOT_DIRECTORY

Control Panel > System > Advanced System Settings > Environment Variables (button) > New System Variable

Variable name : MQSI_FILENODES_ROOT_DIRECTORY
Variable value : C:\Output
