# Demo
Test Doc demo

	
 
  

 















Version	Description	Owner(s)	Date
1.0
Initial draft
Gagan Batra
08/13/21




 
	
Table of Contents
Document Owners	2
Document Status	2
Table of Contents	4
1. Introduction	5
1.1. Overview of Proposed Solution	5
1.2. Business Requirements	5
2. Justification	6
2.1. Current Functionality	6
2.2. Workarounds Considered	7
2.3. Alternative Enhancements Considered	7
2.4. Enhancement Benefits	7
3. Detailed Design Specifications	8
3.1. Add parameter for ‘MTO search criteria’	8
3.2. Update product search login on MTO wizard	8
4. Security	10
5. Data Migration	11
6. Assumptions	12
6.1. Configuration	12
6.2. Cross-Functional Implications	12
7. Scenarios & Examples	13

 
1. Introduction
1.1. Overview of Proposed Solution
This enhancement is designed to make a change in search function on MTO wizard so that system should check for no of released product based on ‘Limit number result to’ parameter on search parameter form instead of released prduct and variant.
1.2. Business Requirements
ID	
	

	
2. Justification
Currently, MTO wizard leverage standard D365 quick search behaviour, which searched based on no of released product variant. 
As MTO wizard is fundamentaly different because MTO wizard only returning results by product, not by variant. 
2.1. Current Functionality
In current functionality, STD D365 consider the parameter ‘Limit number result to’ field on search parameter form and filter the product based on the number of product variants. 
 

Sales order line > Quick search

 

Presently, the same quick search has been leveraged on MTO wizard. 

 
2.2. Workarounds Considered
As a workaround, the ‘limit number of results to’ field on the search parameters form can be increased to accommodate for a larger number of product variants. 
2.3. Alternative Enhancements Considered
N/A
2.4. Enhancement Benefits
With the workaround, this is not sustainable as the number of product variants grows with time. So with this enhancement, it is not required to revisit and update the value in the search parameter.







3. Detailed Design Specifications
3.1. Add parameter for ‘MTO search criteria’
Add a new parameter as ‘MTO search criteria in the search parameter form.

Form:			Search parameter
Field name:		MTO search criteria
Field type:		ENUM
Field values:	Produt, Product variant
Default value:	Product
Help text:	If ENUM value is set to ‘Product’ then the system will search on MTO wizard based on release product combination of parameter ‘Limit number result to’. 
And, if the value is set to ‘Product variant’, then the system will follow STD D365 logic of quick search based on product variant in the combination of parameter ‘Limit number result to’.
 
3.2. Update product search login on MTO wizard
Based on the new parameter (as mentioned in section 3.1), follow the below logic.

IF MTO Search criteria 				Set to ‘Product’
Seach the no. of records based on release product and ‘Limit number result to’ i.e. not based on the product variant.
Else IF MTO Search criteria 		Set to ‘Product Variant’
Follow the existing logic.
 
4. Security
Does this design create new Forms or Reports?
Yes	☐
No 	☒
If yes, new security privileges need to be created for Inquire (read) and Maintain (edit) access.

Indicate the duties or roles which should have access and the development team will create new Privileges and associate them. 
Form/Report	Access Level	Duty(s)
	Inquire (read)	
	Maintain (edit)	
5. Data Migration
New fields
Does this design add new fields(s) to a table that will require data import?
Yes	☐
No 	☒
If yes, identify the associated data entity(s) which should be populated
New Field Name	Data Entity Name
	
	

New tables
Does this design add new table(s) which will require data import?
Yes	☐
No 	☒
If yes, list the tables below and new data entity(s) will be created for each
New Table Name	New Data Entity Name
	
	
6. Assumptions
-	There will not be any change in exiting functionality.
6.1. Configuration
6.2. Cross-Functional Implications

7. Scenarios & Examples

