# Digital Marketing Ads Analytics

## Definition
Power BI report/project to consume data from Meta/Facebook Marketing API.


## Power BI Project set up
#### 1) Create the Meta Marketing API app and generate the access token.
* [Meta for Developers: Marketing API docs](https://developers.facebook.com/docs/marketing-apis/?locale=en_US)

#### 2) Re-create or Update the 'expressions.tmdl' file
* With the Power BI project opened, create a file `expessions.tmdl` in the `**.SemanticModel\definition\expressions.tmdl` folder.

* In the `expression access_token` change the placeholder: `<YOUR-APP-ACCESS-TOKEN>` with the access token from your Meta Marketing API app.

* In the `customer_adacounts` adjust the list of values: `{"<ACT_ADCCOUNT1>","<ACT_ADCCOUNT1>", "<ACT_ADCCOUNT1>"}` with the Ad Accounts you want to request the API data. (*Example: {"act_83515351351", "act_81835135154"}*)


```tmdl
expression access_token = "<YOUR-APP-ACCESS-TOKEN>" meta [IsParameterQuery=true, Type="Text", IsParameterQueryRequired=true]
	lineageTag: 1ff2b67c-f2e6-40ee-a884-cba458bc5838
	queryGroup: Parameters

	annotation PBI_ResultType = Text

	annotation PBI_NavigationStepName = Navigation

expression customer_adaccounts =
		let
		    Source = {"<ACT_ADCCOUNT1>","<ACT_ADCCOUNT1>", "<ACT_ADCCOUNT1>"},
		    #"Converted to Table" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
		    #"Changed Type" = Table.TransformColumnTypes(#"Converted to Table",{{"Column1", type text}}),
		    #"Renamed Columns" = Table.RenameColumns(#"Changed Type",{{"Column1", "Customer Ad Account"}})
		in
		    #"Renamed Columns"
	lineageTag: 8606daf1-d4f3-444d-b4fa-007fe856ead3
	queryGroup: Parameters

	annotation PBI_NavigationStepName = Navigation

	annotation PBI_ResultType = Table
```
