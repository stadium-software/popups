# Modal Popups
This module contains three different modal popup variations. Additionally, it describes how to dismiss a popup by clicking on the background

## Description
Modal popups serve to focus the attention of users on a particular UI element. This is done to allow the users to focus on a specific task. Such popups are most appropriate for subtasks, such as adding or updating table rows and returning users back to the previous view. 


https://github.com/stadium-software/popups/assets/2085324/33c1ec7d-1412-4dcb-8a4b-905645e23c5e


## Version
2.0

## Change log
2.0 Added full-page popup and full-page with background popup. Removed Stadium 5 sample. 

<hr>

## Application Setup
1. Check the *Enable Style Sheet* checkbox in the application properties

## Popups

1. [In-Page Popup](#in-page-popup)
2. [FullPage Popup](#fullpage-popup)
3. [FullPage Popup With background](#fullpage-popup-with-background)
4. [Dismiss Click](#dismiss-click)

<hr>

## In-Page Popup 
The in-page popup shows and hides a container on the page as the buttons are clicked. You can use this method when you have smaller pages with few elements. 

### Setup
1. Drag a *Container* control to a page and name it "ModalBackgroundContainer"
2. Add a class called "custom-modal-background" to the "ModalBackgroundContainer" control *Classes* property 
3. Set the *Visible* property of the "ModalBackgroundContainer" control to "false"
4. Drag a container inside the "ModalBackgroundContainer" control and name it "ModalContentContainer"
5. Add a class called "custom-modal-content" to the "ModalContentContainer" control *Classes* property 
6. Drag any controls you wish to display into the ModalContent into the control named "ModalContentContainer"

### EventHandler
1. Drag a *Button* or *Link* control to the page and name it "ModalShowButton"
2. Add a *Click* eventhandler to the "ModalShowButton" control
3. Drag a *SetValue* action into the *ModalShowButton.Click* eventhandler
   1. Name the SetValue "ShowPopup"
   2. Set the Target property to: *ModalBackgroundContainer.visible*
   3. Set the Value property to: *true*
4. Drag a *Button* or *Link* control into the "ModalContentContainer" control and name it "ModalCloseButton"
5. Add a *Click* eventhandler to the "ModalCloseButton" control
6. Drag a *SetValue* action into the *ModalCloseButton.Click* eventhandler
   1. Name the SetValue "HidePopup"
   2. Set the Target property to: *ModalBackgroundContainer.visible*
   3. Set the Value property to: *false*

<hr>

## FullPage Popup
The full-page popup method makes complete pages appear to be popups. These pages use a Template that applies to popup styling to any page. Since Stadium 6 generates a single-page application, no pages are downloaded when users navigate between pages and it is not immediately apparent to the application user that they have navigated to another page. The only difference between this method and an in-page popup is that the opening page is not visible in the background of the popup page.

### Setup
1. Create a new template and name it "PopupTemplate"
2. Drag a *Container* control into the "PopupTemplate" and name it "ModalBackgroundContainer"
3. Add a class called "custom-modal-background" to the "ModalBackgroundContainer" control *Classes* property 
4. Drag a container inside the "ModalBackgroundContainer" control and name it "ModalContentContainer"
5. Add a class called "custom-modal-content" to the "ModalContentContainer" control *Classes* property 
6. Drag the *PageContentPlaceholder* into the "ModalBackgroundContainer" control
7. Assign the "PopupTemplate" to pages to make them appear to be popups

![](images/PopupTemplateView.png)

### Opening and closing a FullPage Popup
Navigate to a popup page to make it appear as if the popup was opened. 

Navigate away from a popup page (usually back to the opening page) to make it appear as if the popup was closed. 

<hr>

## FullPage Popup With Background
The full-page popup with background is essentially the same as the full-page popup, with the exception that a Javascript library called html2canvas is used to take a screenshot of the opening page. That screenshot is then used to make it appear as if the opening page is in the background of the popup page. This screenshot will, however, distort if the viewport size is changed while user views the popup page. 

### Setup
1. Create a folder called JS in the EmbeddedFiles
2. Drag the html2canvas.min.js library file into the folder
3. Add the link below to the *Head* property of the application
```
<script src="{EmbeddedFiles}/JS/html2canvas.min.js"></script>
```
4. In the application properties panel, open the *Variables* property to add a session variable to the application
5. Add a variable called "bgImage" to the application
6. Create a "PopupTemplate" as above
7. Open the the event hander that navigates the user to the popup page (e.g. the button click event handler)
   1. Drag a Javascript action into the script and place it above the NavigateToPage action
   2. Call the Javascript action "CreatePageScreenshot_JS"
   3. Paste the Javascript below into the Code property
```
let img = html2canvas(document.body).then((canvas) => {
   return canvas.toDataURL("image/png");
});
return img;
```
8. You can ignore the error that appears in the validation panel "Invalid script was detected"
9. Drag a SetValue action directly below the "CreatePageScreenshot_JS" action
   1. Set the target property to *Session.Variables.bgimage*
   2. Set the *Value* property to the return value of the "CreatePageScreenshot_JS" action (~.CreatePageScreenshot_JS)
10. In the popup Page.Load event handler
   1. Drag a Javascript action into the script and call it "SetPageBG_JS"
   2. Paste the Javascript below into the Code property
```
let bgColor = getComputedStyle(document.documentElement).getPropertyValue('--modal-background-background-color');
document.querySelector(".custom-modal-background").setAttribute("style", "background-image: linear-gradient(" + bgColor + ", " + bgColor + "), url('"+ Session.Variables.bgImage +"'); background-size: contain; background-repeat: no-repeat; background-position: top center;");
```

## Dismiss Click
Sometimes, it is useful to allow users to click the backdrop to close a modal popup. The dismiss click is quickly and easily performed, which can lead to accidental popup closures. Use this method only when closing the popup by accident does not represent a significant annoyance to the user. 

### Setup
1. Create a script called "DismissPopup"
2. Drag a SetValue into the script and call it "HidePopup"
   1. Set the *Target* property to *ModalBackgroundContainer.Visible*
   2. Set the *Value* property to *false*
3. In the *ModalShowButton.Click* event, drag a Javascript action into the script and add the Javascript below into the *Code* property
```
var th = this;
document.querySelector(".custom-modal-background").addEventListener("click", toggleEventListener);
function toggleEventListener(e) {
	if (e.target.classList.contains("custom-modal-background")) {
		th.DismissPopup();
		e.target.removeEventListener("click", toggleEventListener);
	}
}
```

## Customising the popup
The *modal-variables.css* file included in this repo contains a set of variables that can be changed to customise the modal popup. Follow the steps below to create a custom popup implementation 
1. Open the CSS file called [*modal-variables.css*](modal-variables.css) from this repo in an editor of your choice (I recommend [VS Code](https://code.visualstudio.com/))
2. Adjust the variables in the *:root* element as you see fit

## Applying the CSS
How to apply the CSS to your application
1. Create a folder called *CSS* inside of your Embedded Files in your application
2. Drag the two CSS files from this repo [*modal-variables.css*](modal-variables.css) and [*modal.css*](modal.css) into that folder

#### Stadium 6 (versions 6.6 and above)
2. Paste the link tags below into the *head* property of your application
```
<link rel="stylesheet" href="{EmbeddedFiles}/CSS/modal.css">
<link rel="stylesheet" href="{EmbeddedFiles}/CSS/modal-variables.css">
``` 

## CSS Upgrading
To upgrade thje CSS in this module, follow the [steps outlined in this repo](https://github.com/stadium-software/samples-upgrading)
