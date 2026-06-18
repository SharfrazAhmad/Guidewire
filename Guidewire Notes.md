												Data Model

Delegate entity: 
			A delegate entity in Guidewire is a reusable entity template that defines common fields and behavior. Multiple entities can implement it 	using <implementsEntity>, avoiding duplication and improving maintainability.

			A Delegate Entity is like an interface + shared fields template for entities.
			It:
				Defines common fields
				Defines common methods (via enhancement)
				Can be implemented by multiple entities
			

Non-Persistent Entity: 
		A Non-Persistent Entity is an entity that does NOT have a database table.
		It exists only in memory at runtime and is used mainly for UI, temporary data, or calculations.
		A non-persistent entity is used to hold temporary data and is not stored in the database.


Entities have 3 different extentions:
.eti - 	Entities which are provided ootb by guidewire (under metadata - cannot be modified) and new entities which developer creates (under extension)
.etx - If you want to add a new column to the guidewire provided entity we create extension of eti which is called etx
.eix - platform independent entities which are available to fulfill/support basic necessities of the studio - we cannot modify it


Typelists:
	it contains some predefined set of typecodes or options
	3 extensions same as entity - tti, ttx, tix
	typekey is used to link typelist with entity
	add typecodes to the typelist whenever you want to modify the predefined set of typecodes



**"Whenever you create column of type decimal on any entity - it always needs to have 2 column params"**
			1.Precision
			2.Scale



Foreign Key:
✅ Where do we add a Foreign Key?
👉 Foreign key is always added in the child entity
(i.e., the entity on the “many” side of the relationship)

🎯 Super Simple Trick:
👉 Ask yourself:
“Who needs to remember the parent?”
➡️ That entity gets the foreign key





																	PCF

1.We have 2 pcf elements  
	1.location
	2.widgets 
2. Widgets are sub divided into 2 parts
	1.atomic widget
	2.container widgets 
3.Atomic widgets are sub divided into 3 parts
	1.Cell
	2.Button
	3.Input
4.Container widgets are sub divided into  3 parts
	1.Top level i.e Screen
	2.Secondary level i.e Card view and List Detail view
	3.Primary level i.e list view and Detail View
5Then we have location, inside it we have 
	1.location group
	2.Wizard
	3.Page
	4.Popup
	5.Worksheet
	6.Forward
	7.Exit Point


location:  It is something you can traverse/navigate on.
		left side buttons on policy account 
		eg: Summary, Contacts, Locations...
		every location is associated with a screen

location group: 
		collection of location
		left side buttons on account 
		it doesn't have next and previous buttons on account level
		It is always created under a page

wizard: 	
		location group on policy level are called wizard
		on wizard we have back and next button always where as in account level location group we don't have next and previous buttons
		Every wizard have a screen
		Job wizard are always created under a screen

Popup: 	
		On clicking on one location and going to the another location remembering the previous visited location is called popup
		it has "return to location" button on the top

forward:   
		just like popup, On clicking on one location and going to the another location without remembering the previous screen/location is called forward
		it doesn't have "return to location" button on the top  

Worksheets: 
		Screen popped up from bottom side as a work space is called worksheet
		eg: policy>action>new activity>interview>meet with insured

exit point: 
		on click on any button , it will take you into new website from guidewire
		eg: guidewire>google.com

		
location ref: to add location in location group
panel ref: to add DV/List View  in screen
		def: add DV name
		It is used to add a secondary container widget with the top level container widget


For location/screen we need to add an "entry point" and add a "variable" to hold value 
For widgets we need to create "required variable"  if you need any variable as param

Locations have entry point and Container widget have required variables
Every parameter in entry point should have variable associated with it to store and retain the parameter passed


"required variable" is like a input parameter fed to the screen, the way we pass a parameter to a function, it passes from previous calling screen
"variables" is just like a normal local variable whose scope and initialization is done within the pcf 



Steps to create a pcf:
 Create the entity and  create different columns then add the foreign key inside account 

1. Add a "location ref" in the location group
	 location: add page {eg: training(account)}

2. Create a page
	Entry point: add entry point {eg: training(account:Account)}
	Variable: add a variable {eg: account}
		for every entry point we need to add a variable

3. Add a screen inside a page( Drag Screen ref)
	Required Variable: Enter required variable

 

4. Create Screen  and Add a "panel ref" inside screen to add the DV inside the screen
5. Create Detail View
6.Add the tool bar inside the Screen to get edit buttons(Toolbar is always added to the screen)
7. Add the atomic widget inside the DV
8. Link the atomic widgets with the column of entity inside value
	eg: value= account.calculateFK.number_1

	
Script parameter:


Entity name:


Enhancement:
	Gosu enhancement is code that enhances the functionality of an existing type
	mostly in guidewire studio it is entity but it can be other also
	it it used in modification of functionality of an entity
	Derived value is never saved in database
	Enhancement = methods + getter + setter
	extention: .gsx
	Eg: when age is calculated based on DOB the age is enhancement and age never not be saved in the database. it is just to show on pcf



Popup

	Crate pcf popup
	Enter variable
	Enter entry point:  {signature =same name as popup(variable name: entity type of variable)}
					eg:  TrainingPopup(trainingVar:training)
	Add DV in popup
	Add input in DV
	On click of which atomic widget you want to invoke popup go to that atomic widget property
		action: popup name.push() {Note: popup is invoked using .push() method similarly for forward we use .go() method}
		





Slice Mode and Window mode
	Slice mode can be considered as a policy period slice. It will be having effective and expiration date.
	Window mode - It doesn't consider policyperiod but the entire policy. e.g there can be coverages which are present on the overall term of the 			policy and not on partocular policy periods



											Product Designer





policy lines:

	coverages:
			Terms:
				Options
				Availability
				Offerings:(Which program is offered: eg. Basic, Premium, Standard)

			Reinsurance:

			Availability:
				Availability Script
				Grandfathering States

			Offerings:(Which program is offered: eg. Basic, Premium, Standard)

	Exclusions:
		Terms
		Availability:
			Availability Script
			Grandfathering States

		Offerings:(Which program is offered: eg. Basic, Premium, Standard)

	Conditions:

	Categories:

	Modifiers
		State Mon/Max:
		Availability:
		Offerings:(Which program is offered: eg. Basic, Premium, Standard)








Lookup detail:  Inside Availability (When which date can policy be available)
			If you make a lookup change (availability of the product) for a particular state, once you synchronize product model with policycenter, 			another lookup xml will be created inside the that particular jurisdiction.



System tables
If you want some static data in your project, then you can use system tables. To create a system table, follow below steps. 
	1) Create a new entity, Add columns to it as per the requirements.
	2) Make the entry for that entity in the systables.xml file. Also reference the xml file that you want to add the static data. 
	3) Restart your server.
	4) Open product designer. For that particular system table, you can start adding the data. Once done, you can synchronize the system tables 
	5) Again restart the server.



Availibility Availibility can be set in 3 ways
1) Lookup table-  Use lookup tables if there is a simple requirement
2) Using a availability script - write a custom gosu code if there is a complex logic required to set the availibility 
3) Grandfathering


Grandfathering
Lets say we have a on a policy with base state as AZ that is effective from Jan 01 2024 and has collision coverage on that policy. Now, we made the collision made unavailable in the product designer starting today's date (23/04/2024).
So once the renewal or any transactions happen on this existing policy, the collision coverage will still be available.
But if you initiate a new policy starting 24/04/2024, then in this case, the collision will not be available.


Initialization script - If you want to initialize a term for example to a particular value, you can use initilization script.
Existence Type - Suggested, Electable and Required
Suggested- For a given coverage, if it is selected and chcekbox is checked, then the existence type of that coverage is suggested. 
Electable - If for a given coverage, the checkbox is not checked for that coverage, then the existence type of that coverage is electable. 
Required- If you don't any checkbox around a coverage and still it is on the policy, that particular coverage is requried.


To set the existence type of a coverage, we have to rst of all make the coverage available. Without that, we cannot set the existence type for that coverage. To make the coverage available, we have write the below code.
veh.PALine.getOrCreateCoverage ("PAUIMPDCOV") // Since for Underinsured Motorist Property Damage (PAUIMPDCov), the covered object is PersonalAutoLine

if the covered object is vehicle for a coverage, you can use veh.getOrCreateCoverage (coveragecode)


























Validation:    There are 3 types of validations we can do in policycenter
1) Field Based Validation: We can do it two ways
	 i.FieldValidators.xml
	ii.ValidationExpression-  inside the properties of pcf element

2) Rule Based- when data is committed to the database
3) Class Based Validation



Permission:

Create permission in systempermissiontype.ttx 
Add a Typecode to typelist
Add permisson to some role Provide role to the user 
Use perm.System.Typecode







Batch process:
1.Add type code BatchProcessType
2.Add Categories using BatchProcesstypeUsage(Schedulable, UIRunnable)
3.Create package inside GSRC > GW and create class
4.Extend batch process base inside class
5.Implement the constructor and doWork method in the class and change the access modifier (protected -> public/ default) 
6.Write the business requirement inside doWork method
7.Add your new case inside the ProcessPlugin.gs class


