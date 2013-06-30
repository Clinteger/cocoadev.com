

Defined in <General/AppKit/General/NSNibDeclarations.h> as

    
#ifndef General/IBAction
#define General/IBAction void
#endif


Used as void and serves to alert Interface Builder that said message is an action for target/action connections.

----

**Usage**

    
@interface className
{
//...
}
- (General/IBAction)message:(id)sender;
//...
@end


**Note**:
Interface Builder may not recognize the action if you put a space between     (General/IBAction) and the method name in your header file.
(I have never seen this, and I almost always put some whitespace after (General/IBAction). Thus maybe this pertains to an older version of IB that predates Xcode? --General/GrahamCox)

----

See also General/IBOutlet.

----
**Discussion**

Does anybody else feel that this is slightly clumsy compared to the rest of General/ObjectiveC? Sure, it's marginally convenient, but it goes against the standard form of a function. Creating synonyms for     void seems dangerous, at least to me; a newcomer would think that the method returned some form of action. At least General/IBOutlet is used in the same way as other variable modifiers. --General/JediKnil

*Any newcomer should of course read General/ObjC.pdf, or whatever the file is now; IIRC that file describes the use of     General/IBAction. Nonetheless, it is a bit curious.*

In the "Fundamentals of Cocoa" session at WWDC 2004, the presenter indicated that     General/IBAction was not needed in most cases for IB to notice a method as an action. Simply having the correct signature (returning void with a single id parameter) is sufficient. I have not been able to find any corroborating documentation, but I can confirm that IB seems to recognize my actions just fine even when I don�t tag them with     General/IBAction. --General/KevinYank