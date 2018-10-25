## Import WriteToFile project in App Connect Toolkit

- Open App Connect Enterprise Toolkit. Clic on App Connect Enterprise Toolkit icon

- Import project named `WriteToFile` in workspace
	- Menu > File > Import > Project Interchange > From zip file > Browse (button)
	- Select file : C:\Student\ACE11\Lab Resources\WriteToFile_PI.zip

![](./img/importprojectintoolkit.gif)


## Deploy WriteToFile to App Connect TESTNODE

- Right clic `WriteToFile` project and `Deploy`
- Select **TESTSERVER**

![](./img/deployprojecttonode.gif)


## Open App Connect Web UI

- In App Connect Toolkit 
- Right clic on `TESTNODE` and `Start Web User Interface`

![](./img/openwebui.gif)


## Import Callable flow WriteToFile in App Connect Designer

Go back in App Connect Designer in IBM Cloud

In IBM AppConnect menu > Manage Callable Flow > Connect Callable flow

Clic on button `Download the Configuration` and Save file

Copy the saved file (agentx.json) in the Directory C:\ProgramData\IBM\MQSI\config\TESTNODE\TESTSERVER\iibswitch\agentx  of your "On Premise" App Connect component.

![](./img/importcallableflow.gif)


And Clic on button `Test your agent`

![](./img/testagent.png)

- Clic on `close` button and retunr on Dashboard and Go back to the Callable flow page to refresh it.

If all id OK, you have a new entry in the list :

![](./img/import-callableflow-writetofile.png)

### (Optionnal) Set MQSI root directory environment variable

> 
Set Root Directory environment variable : MQSI_FILENODES_ROOT_DIRECTORY

> Control Panel > System > Advanced System Settings > Environment Variables (button) > New System Variable

>Variable name : MQSI_FILENODES_ROOT_DIRECTORY
>
>Variable value : C:\Output


## Create a new Event Drive Flow

- Clic on Dashboard item

![](./img/godashboard.gif)

- Clic button `New`and select `Event-Driven flow`

![](./img/newevent.gif)

- Give a name to this new workflow
- Add SalesForce `New Lead` action

![](./img/addslfaction.gif)

- Add Callable Flow `WriteToFile` invoke

![](./img/addcallableflow.gif)

- Customize Callable Flow action

![](./img/customizecallableflow.gif)
![](./img/customizecallableflow2.gif)

- At the end the result will be something like that

![](./img/callablesummary.png)

- Next add Salesforce “Update lead” action

	- The final action updates the new lead in Salesforce with data sent back from the called flow running in ACE. 
	- This data is mapped out of the returned local environment from the callable flow.

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

![](./img/newlead.png)

- Save

- Check your flow is running successfully

![](./img/checkruning.png)

- Check you have a new file in you output directory with information about the lead you created previously.

- Check the description in the Lead in Salesforce is updated with information about file creation

![](./img/updatelead.png)

The video below show all steps :

![](./img/createlead.gif)
 