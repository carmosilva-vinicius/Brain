The UI API exposes user interface elements of the SAP Business One front-end, implemented as Distributed Component Object Model (DCOM). One instance of DCOM for UI API is running per Windows session, which is used by all instances of the SAP Business One client running on the same user session.

UI API provides access  to the user elements exposed in the SAP B1 app, making it possible to modify the menus, create new forms and perform the data binding. 
It also has event sink layer which capture UI events provided by SAP B1, allowing the add-on application to react from user interactions with the SAP Business One application.
### UI API Solution Architecture
![[ui-api-arch.png]]

## UI API Objects
The connection object are SboGuiAPI and Application objects. The Desktop represents the SAP Business One desktop (main window). Menus Collection represents a menu, that is, a collection of MenuItem objects.
Forms collection is a collection of Form objects. This object holds all the open forms in the application. The controls on the forms are called Items and are encapsulating multiple child object like, ComboBox, EditTex and so on. The DataSources are creating the link between the Items and database layer.
![[ui-api-objects.png]]
## Add-On Life Cycle
The user login to the SAP Business One client. Afterwards the registered add-on solution is started. The timeout limit is approximately 10 seconds.
The add-on execution requires the Connection String property filled as a command line argument.
The SAP Business One client and the add-on solution is running in parallel.
If the user performs the SAP Business One client shutdown, the add-on must be able to handle the event in order to terminate the add-on solution as well.
![[add-on-lifecycle.png]]

