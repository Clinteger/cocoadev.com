

isDocumentEdited is not set when you use the default undo/redo of General/NSDocument in case the file is saved and the cursor is set to the end of the document.

To reproduce this, simply create a default Cocoa document based application:
-  add an General/NSTextview to the window
-  create an outlet and implement dataRepresentationOfType in your General/MyNSDocument class like something here below.
- set allow undo for the General/NSTextView.

To test, run the program, in the new window, hit enter a few times and save the untitled document.
Now use the arrow down key until you are at the end of the document. Now hit enter or any key and you will see that the text is not marked as modified (red led on the close window button).
It might be that you have to save and move to the end a few times before it happens but I can reproduce it every time.

My question is simple: is this a bug and/or how to fix this.

    

- (General/NSData *)dataRepresentationOfType:(General/NSString *)aType
{
   return General/textView string] dataUsingEncoding: [[NSMacOSRomanStringEncoding allowLossyConversion:YES];
}