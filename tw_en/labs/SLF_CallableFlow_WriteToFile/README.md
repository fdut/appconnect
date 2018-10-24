## Import Callable flow WriteToFile

In App Connect Designer

IBM AppConnect > Manage Callable Flow > Connect Callable flow

Clic on button `Download the Configuration` and Save file

Copy the saved file (agentx.json) in the Directory C:\ProgramData\IBM\MQSI\config\TESTNODE\TESTSERVER\iibswitch\agentx  of your "On Premise" App Connect component.

And Clic on button `Test your agent`


### Set MQSI root directory environment variable

> 
Set Root Directory environment variable : MQSI_FILENODES_ROOT_DIRECTORY

> Control Panel > System > Advanced System Settings > Environment Variables (button) > New System Variable

>Variable name : MQSI_FILENODES_ROOT_DIRECTORY
>
>Variable value : C:\Output
