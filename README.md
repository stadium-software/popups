# Popups
Simple modal popup implementation

## Description
Modal popups serve to focus the attention of users on a particular UI element. This is done to allow the users to focus on a specific task. Modal popups are most appropriate for subtasks, such as adding or updating table rows and returning users back to the previous view. 

## Page Setup
1. Check the *Enable Style Sheet* checkbox in the application properties
2. Drag a *Container* control to a page and name it "Overlay"
3. Add a class called "overlay" to the "Overlay" control *Classes* property 
4. Set the *Visible* property of the "Overlay" control to "false"
5. Drag a container inside the "Overlay" control and name it "Popup"
6. Add a class called "popup" to the "Popup" control *Classes* property 
7. Drag any controls you wish to display into the popup into the control named "Popup"

## EventHandler Setup
1. Drag a *Button* or *Link* control to the page and name it "OpenPopup"
2. Add a *Click* eventhandler to the "OpenPopup" control
3. Drag a *SetValue* action into the *OpenPopup.Click* eventhandler
   1. Set the Target property to: *Overlay.visible*
   2. Set the Value property to: *true*
4. Drag a *Button* or *Link* control to the page and name it "ClosePopup"
2. Add a *Click* eventhandler to the "ClosePopup" control
3. Drag a *SetValue* action into the *ClosePopup.Click* eventhandler
   1. Set the Target property to: *Overlay.visible*
   2. Set the Value property to: *false*

## StyleSheet CSS
Paste the CSS below into the StyleSheet and adjust the variables in the *:root* element as you see fit
```
:root {
    --overlayBackgroundColor: rgba(0,0,0,0.5);
    --popupBackgroundColor: #ffffff;
    --popupBorderColor: #2196f3;
    --popupShadowColor: rgba(0, 0, 0, 0.45);
}
.overlay {
	position: fixed;
	display: grid;
	place-items: center;
	top: 0;
	left: 0;
	bottom: 0;
	right: 0;
	background-color: var(--overlayBackgroundColor);
}
.popup {
	background-color: var(--popupBackgroundColor);
	border-radius: 6px;
	border: 1px solid var(--popupBorderColor);
	padding: 20px;
	box-shadow: var(--popupShadowColor) 0px 5px 15px;
	overflow: auto;
	max-height: 85vh;
}
```