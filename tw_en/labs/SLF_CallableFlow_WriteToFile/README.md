# App Connect : Even-driven flow using an ACE callable flow


Your company is starting to use Salesforce for its Sales reps to record customer leads that they find. 

In the past, all customer-related sales information has been stored in an on-premises custom sales application. 

The on-premises system still needs to have a record of all the leads found by the sales reps, but they don’t want to have to enter the data in both systems. 

In time, the Salesforce system will take over more and more of the on-premises application processing but for now, both applications need the lead information. 

Integrating these two systems requires a hybrid integration approach where some of the integration function runs in the cloud and some must run on premises. 

App Connect Enterprise provides exactly this capability, being able to split the integration seamlessly between the cloud and on-premises system, without the need to define special interfaces or expose the on-premises system directly to the public internet.


![](./img/diagram.jpg)

In this tutorial you learn how to use IBM App Connect Enterprise to create an event-driven flow that creates a lead in an on-premises sales system with a file-based interface whenever a lead is created in Salesforce.

![](./img/evendrivenflow.png)

## Import WriteToFile project in App Connect Toolkit


- in the VM, open the **App Connect Enterprise Toolkit**

	- Clic on App Connect Enterprise Toolkit icon

- Import project named `WriteToFile` in workspace
	- Menu > File > Import > Project Interchange > From zip file > Browse (button)
	- Select file : C:\Student\ACE11\Lab Resources\WriteToFile_PI.zip

![](./img/importprojectintoolkit.gif)


## Deploy WriteToFile to App Connect TESTNODE

- Right clic `WriteToFile` project and `Deploy`
- Select **TESTSERVER**

![](./img/deployprojecttonode.gif)


## Open App Connect Enterprise Web UI

- In App Connect Toolkit 
- Right clic on **`TESTNODE`** and **`Start Web User Interface`**

![](./img/openwebui.gif)


## Import "WriteToFile" Callable flow in App Connect Designer on IBM Cloud

- From a brower in your VM, connect to your IBM App Connect environnement in IBM Cloud

	In **IBM AppConnect** **Menu > Manage Callable Flow > Connect Callable flow**

- Clic on button **`Download the Configuration`** and Save file

- Copy the saved file (agentx.json) in the Directory 

	`C:\ProgramData\IBM\MQSI\config\TESTNODE\TESTSERVER\iibswitch\agentx`  of your "On Premise" App Connect component.


![](./img/importcallableflow.gif)

- Stop the **TESTSERVER**

![](./img/stoptestserver.png)

- Start the **TESTSERVER**

![](./img/starttestserver.png)


- From the brower in your App Connect Popup, Clic on button `Test your agent`

![](./img/testagent.png)

- Clic on `close` button and retunr on Dashboard and Go back to the Callable flow page to refresh it.

	If all is OK, you have a new entry in the list :

![](./img/import-callableflow-writetofile.png)


## Create a new Event Drive Flow

- From your App Connect environnement on IBM Cloud, Clic on Dashboard item

![](./img/godashboard.gif)

- Clic button `New`and select `Event-Driven flow`

![](./img/newevent.gif)

- Give a name to this new workflow

- Add **SalesForce `New Lead`** action

![](./img/addslfaction.gif)

- Add Callable Flow `WriteToFile` invoke

	- **Application : WriteToFile**
	- **Endpoint : WRITE_TO_FILE**

![](./img/addcallableflow.gif)

- Customize Callable Flow action
- Add FileName and DirectoryName properties

	- **FileName** : **demo.xml**
	- **DirectoryName** : **/fileout**


![](./img/customizecallableflow.gif)

- Add properties for content of the "On-premise" file 

	- **FirstName** : **(Salesforce) First Name**
	- **LastName** : **(Salesforce) Last Name**
	- **Company** : **(Salesforce) Company**
	- **Email** : **(Salesforce) Email**


![](./img/customizecallableflow2.gif)

- At the end the result will be something like that

![](./img/callablesummary.png)

- Next add Salesforce “Update lead” action

	- The final action updates the new lead in Salesforce with data sent back from the called flow running in ACE. 
	- This data is mapped out of the returned local environment from the callable flow.

	Update the following values
	
	- (Salesforce) Lead ID  equals **(Salesforce) Lead ID**

	- **(Salesforce) Description** : **LeadId: (Callableflow) LocalEnvironnement.Variables**


![](./img/addlaststep.gif)

When you’ve checked everything in the flow (including changing the directory and file name to valid values), open the options menu [⋮] in the banner and click Start flow. 

![](./img/startflow.gif)

Then click Dashboard to exit the flow. The flow is now running and ready to be triggered by a new lead in Salesforce.


## Finally, test your flow

- Create a new Salesforce lead:

- Log in to Salesforce using the account that’s connected to IBM App Connect.

- Create a new lead, specifying values for First Name, Last Name, Company, and Email; for example:

Field | Value
------------- | -------------
FirstName | Jean
LastName  | DUBOIS
Company  | ACME
Email | jean.dubois@acme.com

![](./img/newlead.png)

- Save

- Check your flow is running successfully

![](./img/checkruning.png)

- Check you have a new file in you output directory with information about the lead you created previously.

- Check the description in the Lead in Salesforce is updated with information about file creation

![](./img/updatelead.png)

The video below show all steps :

![](./img/createlead.gif)
 
 Congratulation, you created successfully your first Even Driven Flow.
 
# Summary
---
 
During this exercise we created and tested an Event Driven flow with "On-premise" integration


Now you have learned the process to build a simple App Connect Flow and using an ACE callable flow to augment the input data.

You can take this same process to build more complex business solutions using the wide array of applications available in IBM App Connect.
 
 
# Resources :
---

https://developer.ibm.com/integration/docs/app-connect-enterprise/tutorials/exchange-data-cloud-saas-applications-premises-activities-using-ace-callable-flow/

