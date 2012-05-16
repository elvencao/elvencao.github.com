---
layout: post
title: "How to elegantly replace iPhone keyboard with UIDatePicker"
date: 2012-05-16 15:32
comments: true
categories: [iOS]
---
How can I display a date picker controller instead of default keyboard on tap of a text field?  
`UITextField` is a subclass of `UIResponder`, which means it has a `inputView` property. Just 
simply create a `UIDatePicker`, set it to be the text field's `inputView`, and that's done.  
It also has a `inputAccessoryView` property. This can be used to be set with a toolbar view 
and also with some toolbar buttons to perform done or cancel accessory operations.   
**Example**  
``` objective-c   
@interface CustomKeyboardAppDelegate : NSObject <UIApplicationDelegate> {  
...  

@property (nonatomic, retain) IBOutlet UIWindow *window;  
@property (nonatomic, retain) IBOutlet UITextField *textField;  
@property (nonatomic, retain) IBOutlet UIToolbar *accessoryView;  
@property (nonatomic, retain) IBOutlet UIDatePicker *datePicker;  

- (IBAction)doneEditing:(id)sender;  
- (IBAction)cancelEditing:(id)sender;   
@end  
```   
In Interface Builder, pull out `UIDatePicker` and `UIToolbar` to the controller's scene dock 
(not the controller's view scene). And then pull out two toolbar buttons for done and cancel 
into toolbar. Connect the outlets appropriately. Connect `Cancel` button to `cancelEditing` 
and `Done` button to `doneEditing`. `Done` button will set the seleted date value to the 
text field and then dissmiss date picker. `Cancel` button will just dismiss date picker. 
The methods are implemented as listed below.   
``` objective-c   
@implementation CustomKeyboardAppDelegate   

@synthesize window=_window;  
@synthesize textField = _textField;  
@synthesize accessoryView = _accessoryView;  
@synthesize datePicker = _datePicker;  

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions  
{  
    self.textField.inputView = self.datePicker;  
    self.textField.inputAccessoryView = self.accessoryView;  
    ...    
}  

...  

- (IBAction)doneEditing:(id)sender {  
	self.textField.text = [NSString stringWithFormat:@"%@", datePicker.date];  
    [self.textField resignFirstResponder];  
}  

- (IBAction)cancelEditing:(id)sender {
	[self.textField resignFirstResponder];  
}
@end  
```   
Setting the `autoresizingmask` of the `UIDatePicker` can make it work in landscape.    
{% codeblock lang:objc %}
datePicker.autoresizingMask = (UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight);  
{% endcodeblock %}   
__References on Stackflow__  
1. [Display datepicker on tapping on textfield](http://stackoverflow.com/questions/6074683/display-datepicker-on-tapping-on-textfield)  
2. [iPhone: Can I make a UIDatePicker appear on top of a UIKeyboard?](http://stackoverflow.com/questions/7721926/iphone-can-i-make-a-uidatepicker-appear-on-top-of-a-uikeyboard)  
__Other articles that are not praticed__  
1. [Elegantly replace iPhone keyboard with UIPickerView](http://stackoverflow.com/questions/1275633/elegantly-replace-iphone-keyboard-with-uipickerview)  
2. [UIDatePicker pop up after UIButton is pressed](http://stackoverflow.com/questions/4824043/uidatepicker-pop-up-after-uibutton-is-pressed)  
3. [How can I present a picker view just like the keyboard does?](http://stackoverflow.com/questions/6269244/how-can-i-present-a-picker-view-just-like-the-keyboard-does)  


