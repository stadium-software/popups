# Modal Popups
This module contains three different modal popup variations. Additionally, it describes how to dismiss a popup by clicking on the background

## Description
Modal popups serve to focus the attention of users on a particular UI element. This is done to allow the users to focus on a specific task. Such popups are most appropriate for subtasks, such as adding or updating table rows and returning users back to the previous view. 

https://github.com/stadium-software/popups/assets/2085324/1a071448-f4c1-41bd-abbc-5bb75cd3c28c

## Sample applications
This repo contains one Stadium 6.7 application
[ModalPopups.sapz](Stadium6/ModalPopups.sapz?raw=true)

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
3. [Dismiss Click](#dismiss-click)

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
The full-page popup method makes complete pages appear to be popups. These pages use a Template that applies to popup styling to any page. Since Stadium 6 generates a single-page application, no pages are downloaded when users navigate between pages and it is not immediately apparent to the application user that they have navigated to another page. The only difference between this method and an in-page popup is that the opening page is not visible in the background of the popup page. Considering that users cannot interact and do not need the background page, this method has the significant advantage that there are significantly fewer elements to consider when developing a page. 

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

## Dismiss Click
Sometimes, it is useful to allow users to click the backdrop to close a modal popup. The dismiss click is quickly and easily performed, which can lead to accidental popup closures. Use this method only when closing the popup by accident does not represent a significant annoyance to the user. 

### Setup
1. Create a script called "DismissPopup"
2. Drag a SetValue into the script and call it "HidePopup"
   1. Set the *Target* property to *ModalBackgroundContainer.Visible*
   2. Set the *Value* property to *false*
3. In the *ModalShowButton.Click* event, drag a Javascript action into the script and add the Javascript below into the *Code* property
```javascript
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
```html
<link rel="stylesheet" href="{EmbeddedFiles}/CSS/modal.css">
<link rel="stylesheet" href="{EmbeddedFiles}/CSS/modal-variables.css">
``` 

## CSS Upgrading
To upgrade thje CSS in this module, follow the [steps outlined in this repo](https://github.com/stadium-software/samples-upgrading)
