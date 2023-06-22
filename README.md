# myppjourney
My Power Platform Journey


Git Version Control: https://www.matthewdevaney.com/allow-multiple-power-apps-developers-to-simultaneously-edit-canvas-apps/

Career Robot: https://github.com/WKahnZA/AIPrompts/blob/main/Career%20and%20Professional%20Development/CareerGPTv2.md

*PowerApp: How to clear text input fields?*

There are several ways to clear text input fields in PowerApps. One way is to use the Reset function on a button, which will clear the text input and show the default value or hint text1. Another way is to use the Clear field option in the properties of the text input, which will display an “X” when the field is in focus and allow the user to clear the field by clicking on it2.

You can also clear the text input using context variables. Set the Default property of the text box to a variable and use the UpdateContext function on the OnSelect property of the submit button1. You can also set the Default property to a value that will reset the input, such as an empty string1. Finally, you can create a variable and use it in the Reset property of the text input, and then update the variable using the UpdateContext function1.

Component Library: A component library provides a centralized and managed repository of components for reusability.

How to create Menu Components: https://www.matthewdevaney.com/power-apps-navigation-menu-component/ 
How to create Labels and Buttons: XXX

Security Concept for Dataverse: https://docs.microsoft.com/en-us/power-platform/admin/wp-security-cds

How to hide content from screen-reader or sighted users: https://learn.microsoft.com/en-us/power-apps/maker/canvas-apps/accessible-apps-content-visibility

About Tables:

In Power Apps, you can create different types of tables: Standard, Activity, Virtual, and Elastic1.

*Standard tables* are included with a Power Platform environment that includes Microsoft Dataverse. Account, business unit, contact, task, and user tables are examples of standard tables in Dataverse. Most of the standard tables included with Dataverse can be customized1.

*Activity tables* are a special kind of table that is best for rows that have an activity-based element, which can include a subject, start time, stop time, due date, and duration. Dataverse already comes with several out-of-the-box activity tables, such as appointment, task, email, and phone call1.

*Virtual tables* enable the integration of data residing in external systems by seamlessly representing that data as tables in Microsoft Dataverse, without replication of data and often without custom coding2.

*Elastic tables* are for when the table will store a very large dataset in excess of tens of millions of rows1.

The main advantage of *user or team owned records* is that it allows for more granular control over access to the data. Actions that can be performed on these rows can be controlled on a user level1. This means that you can restrict access to certain records to specific users or teams2.

The main advantage of *organization owned records* is that the security checks are simpler and faster, as access to the data is controlled at the organization level3.

However, some people have used organization owned records and lived to regret it, as it can be difficult to restrict access to certain records once broad organization level read access has been granted2.
