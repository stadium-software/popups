# Modal Popups
Simple modal popups for Stadium 5 and 6

## Description
Modal popups serve to focus the attention of users on a particular UI element. This is done to allow the users to focus on a specific task. Such popups are most appropriate for subtasks, such as adding or updating table rows and returning users back to the previous view. 

https://github.com/stadium-software/ModalContents/assets/2085324/215c2899-b09f-4286-b412-cde8be4a72c8

## Version
1.0

## Application Setup
1. Check the *Enable Style Sheet* checkbox in the application properties

## Page Setup
1. Drag a *Container* control to a page and name it "ModalBackground"
2. Add a class called "custom-modal-background" to the "ModalBackground" control *Classes* property 
3. Set the *Visible* property of the "ModalBackground" control to "false"
4. Drag a container inside the "ModalBackground" control and name it "ModalContent"
5. Add a class called "custom-modal-content" to the "ModalContent" control *Classes* property 
6. Drag any controls you wish to display into the ModalContent into the control named "ModalContent"

## EventHandler Setup
1. Drag a *Button* or *Link* control to the page and name it "OpenModal"
2. Add a *Click* eventhandler to the "OpenModal" control
3. Drag a *SetValue* action into the *OpenModal.Click* eventhandler
   1. Set the Target property to: *ModalBackground.visible*
   2. Set the Value property to: *true*
4. Drag a *Button* or *Link* control to the page and name it "CloseModal"
2. Add a *Click* eventhandler to the "CloseModal" control
3. Drag a *SetValue* action into the *CloseModal.Click* eventhandler
   1. Set the Target property to: *ModalBackground.visible*
   2. Set the Value property to: *false*

## StyleSheet CSS
1. Open the CSS file called *modal-variables.css* from this repo in an editor of your choice (I recommend [VS Code](https://code.visualstudio.com/))
2. Adjust the variables in the *:root* element as you see fit

## Applying the CSS
How to apply the CSS to your application

### Stadium 6 (versions 6.6 and above)
1. Add the two CSS files to the Embedded Files of your application
2. Paste the link tags below into the *head* property of your application
```
<link rel="stylesheet" href="{EmbeddedFiles}/modal.css">
<link rel="stylesheet" href="{EmbeddedFiles}/modal-variables.css">
``` 

### Stadium 5
Add a Javascript action into the Page.load event handler and paste the Javascript below into the Code Editor popup
```
let URL = window.location.protocol + "//" + window.location.host + "/" + window.location.pathname + "//";
let el1 = document.createElement("link");
el1.setAttribute("rel","stylesheet");
el1.setAttribute("href",URL + "Content/EmbeddedFiles/modal.css");
document.querySelector("head").appendChild(el1);
let el2 = document.createElement("link");
el2.setAttribute("rel","stylesheet");
el2.setAttribute("href",URL + "Content/EmbeddedFiles/modal-variables.css");
document.querySelector("head").appendChild(el2);
``` 

## Upgrading
To upgrade this module
1. Pull the latest repo
2. If you have made changes to the *modal-variables.css* file in your local repo, merge them
3. You can drag the *modal.css* file into the EmbeddedFiles folder of your application as is
4. Select "Overwrite" when prompted in Stadium
5. Open the *modal-variables.css* file 
6. If new variables were added, change the variables as you see fit 
7. Drag the updated *modal-variables.css* file into the EmbeddedFiles folder of your application