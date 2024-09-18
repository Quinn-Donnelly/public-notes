Parent:: [[Android Development]]
supports:: [[MOC Event Driven System Test.canvas|Event Driven System Test]]
# Summary 
Learning how the android assistant launches apps and integrates parameters from voice. 
# Body
They register under a [[Built in Intents]] or [[BII]] then when assistant has a query that it matches to [[BII]]. There are also [[Custom Intents]] but they recommend using [[BII]] first

Users can create shortcuts which will allow the user to define a custom phrase to a deeplink with prefilled information to one of the above input types. 

App registers with the device a capabilities.xml files to register which intent you handle and map the parameters to internal structures.