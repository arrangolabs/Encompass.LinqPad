# Encompass.LinqPad
LinqPad queries and classes for Ellie Mae Encompass Loan Origination System (LOS)

## Installation

For these queries to function you must have access to an Encompass LOS System and have the appropriate Encompass SDK version for that server instance. If you've never installed the SDK you may also need to talk to your EllieMae rep to obtain some license keys. You can obtain a SDK from the following: http://download.elliemae.com/encompass/updates/18.1.0/encompass181sdk.exe, just substitute the appropriate version numbers. If you get a VersionException you'll know you have the wrong SDK installed. If you have multiple versions installed on your servers then you will have to use a VirtualBox setup to have both installed (See the Advanced Install below).

The MyExtensions LinqPad file will need to go into your MyExtensions file in the plugins directory for your LinqPad installation (see your Folder settings in Preferences) or you can just overwrite with this one if you haven't modified your own.

The references should all be standard for a normal Encompass install but you may have to tweak them to fit your system (F4). The NUnit and NUnitLite references are not strictly needed but it's great for testing.

Once you've updated the MyExtensions file to your plugins folder you'll need to edit the file and update the user names("YourUserNameHere") and server Id's("YourServerIdHere") for your Encompass servers. There are 4 instances, (Develop, Test, Staging, Production), defined by the Factory class but you may have only one server in your environment. If you only have one then use Production. Use as many of the defined instances as needed for your environment. You can comment out the others.

Once you've edited the file try running the file. LinqPad should prompt you for password's for the environment you are trying to connect to. If not make sure you update the passwords in LinqPad's Password Manager.

A typical run looks something like the following:
![Field Search Results](docs/field_search_results.png)

The benefits of this search are that you get to see the field values as well as the display text.
![Field Values](docs/field_search_values_results.png)

You can also display the Reporting Database fields by changing the code to look like the following:
```
var found = Factory.SearchReportingFields(fields).OfType<ReportingFieldDescriptior>()
  .Where(f => f.FieldID.Contains("Appraisal".ToUpper()))
	.OrderBy(f => f.FieldID)
	.Select(f => new
		{
			FieldId = f.FieldID,
			Format = f.FieldType,
			Name = f.CanonicalName,
			Description = f.Description,
			Table = f.TableName,
			Column = f.ColumnName
	})
	.Dump();
```
Results should look something like the following:
![Reporting Field Search Results](docs/reporting_field_search_results.png)

## Advanced Install

## References
Encompass - https://www.elliemae.com/encompass/encompass-overview

SDK Downloads - https://resourcecenter.elliemae.com/resourcecenter/Downloads.aspx

SmartClient - https://elliemae.com/getencompass360
