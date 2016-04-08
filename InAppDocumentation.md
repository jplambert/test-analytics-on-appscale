# Introduction #

This page details how to use the Test Analytics application.  For more information on the ACC methodology that Test Analytics uses, see [AccExplained](AccExplained.md).

## Project Details ##

These details help identify your project. You can also edit the name of the project here.

**Permissions**: Project owners can edit any ACC data, delete the project, or make the project public. Editors can edit ACC data. Viewers can see the ACC model, but not make any changes.

**Public access**: If a project is marked public, anybody can view the project as if they were listed on the project as a viewer. It may also appear on the Test Analytics homepage to the world.

## Attributes ##

Attributes are the adjectives that describe your project. Common attributes include "Secure" and "Fast". Typically, a product manager or tester with high knowledge of the product will have a hand in narrowing down the list of attributes for the system.

For more information on the ACC methodology that Test Analytics uses, see [AccExplained](AccExplained.md).

## Components ##

Components are the nouns that are parts of your project -- the building blocks that constitute the system in question. Examples could include "Firmware", "Shopping Cart" or "Database".

For more information on the ACC methodology that Test Analytics uses, see [AccExplained](AccExplained.md).

## Capabilities ##

Capabilities are the verbs of your project. They describe the abilities of a component required to satisfy an attribute of a system. In an example of a e-commerce website, which would have an attribute "Secure" and a component "Shopping Cart", might have a capability "Process monetary transactions using HTTPS".

For more information on the ACC methodology that Test Analytics uses, see [AccExplained](AccExplained.md).

## Configuring Data Requests ##

Test Analytics can have risk data brought in from external sources, such as bug trackers or test case managers. These data points can then be used to quantify the risk in your ACC model. Here, you can add a request from a supported data source and configure what data should be imported.

For example, you could add an Issue Tracker data source, which is configured to bring in issues under a specific project, and marked with a specific label.

Once you are importing data, you can use filters to automatically assign attributes, components, or capabilities to data as it is imported.

## Filters ##

Filters allow you to assign attributes, components, and capabilities to your bugs, checkins, or test results as they are imported. You can filter on various options, such as title or labels.

## Project Bugs, Checkins, and Testcases ##

This page allows you to see an overview of the data in your system, and which data has been assigned to your ACC model.

## Risk ##

This allows you to visualize the risk of your project based off your assigned inherent risk, as well as the data you've imported into Test Analytics.