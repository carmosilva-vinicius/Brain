## Object Categories

▪ Business Objects
	▪ Master Data Objects
		▪ BusinessPartners
		▪ Items
		▪ …
	▪ Transactional Data Objects
		▪ Journal Entries
		▪ Documents: Order, Invoice,…
		▪ …
▪ Infrastructure Objects
	▪ Company object
	▪ Extended Functionality Objects
		▪ RecordSet
		▪ DataBrowser
		▪ SBObob
	▪ Meta Data Objects
		▪ UserTablesMD
		▪ UserKeysMD
		▪ UserFieldsMD
		▪ UserObjectsMD
▪ Special Objects
	▪ Service Type Objects
		▪ CompanyService
		▪ AccountsService
		▪ BusinessPartnersService
		▪ FormPreferencesService
		▪ MessagesService
		▪ ReportLayoutsService
		▪ SeriesService
		▪ ...
	▪ Definition Objects related to SAP
	Business One GUI
		▪ ChooseFromList
		▪ DynamicSystemStrings
		▪ Formatted Searches
		▪ MultiLanguageTranslations
		▪ UserQueries
## Database Connection
Follow these steps to establish a connection to a database:
▪ First define a variable for the Company object.
▪ Then initialize the Company object.
▪ After that define the contention properties in the Company object.
▪ Alternatively you can set the Add-On identifier if you like to have a
unique string identifier for your add-on solution.
▪ Then the Connect method should be called, which connects to the
SAP Business One company database.
▪ At the end, an error handling execution might appear.
```cs
SAPbobsCOM.Company oCompany = new SAPbobsCOM.Company();
try {
	oCompany.Server = "dbservername";
	oCompany.CompanyDB = "dbname";
	oCompany.DbUserName = "sa";
	oCompany.DbPassword = "dbpassword";
	oCompany.UserName = "user";
	oCompany.Password = "userpass";
	oCompany.DbServerType = SAPbobsCOM.BoDataServerTypes.dst_MSSQL2019;
	oCompany.UseTrusted = true;
	
	int ret = oCompany.Connect();
	string errMsg = oCompany.GetLastErrorDescription();
	int ErrNo = oCompany.GetLastErrorCode();
	if(ErrNo != 0)
	{	
		Console.WriteLine(errMsg);	
		MessageBox.Show($"Error: {errMsg}");	
	}	
	else
	{	
		MessageBox.Show("Success connected");
	}	
}	
catch (Exception errMsg)	
{
	throw errMsg;
}
```

## Business object
Examples of business objects include the following:
▪ Item master data
▪ Business partner master data
▪ Product tree objects
▪ Documents (for example, Sales and Purchasing documents)
▪ Payments object