[http://developer.apple.com/documentation/Cocoa/Reference/General/ApplicationKit/ObjC_classic/Classes/General/NSFont.html]

The General/NSFont class represents the fonts installed on a system to an application. You don't create General/NSFonts with alloc/init, but instead use     General/NSFont fontWithName: (General/NSString *)fontName size: (float)size to search for fonts with a particular name, or you can use     General/[NSFont systemFontOfSize:(float)size],     General/[NSFont userFixedPitchFontOfSize:(float)size],     General/[NSFont labelFontOfSize:(float)size] and similar methods (see the General/NSFont docs) to retrieve standard system fonts. If you pass 0 or a negative number for any of the size params, you'll get the default size for that particular font. 

I'm not 100% positive on this, but I also don't think you can archive General/NSFont objects using General/NSArchiver. Actually, you can archive them, but if you try to use the unarchived General/NSFont object, you'll crash. Instead, save the General/NSString returned from     General/[NSFont fontName] and load it up again with     General/[NSFont fontWithName: fontName size:size].

*I use archived fonts in my app for storing the user's choice, and it works just fine. You must have been doing something wrong.*

This works because General/NSCoder provides a means of substituting one object for another upon unarchiving. The 'real' General/NSFont instance is substituted for the one being unarchived. See [http://developer.apple.com/documentation/Cocoa/Conceptual/Archiving/Tasks/codingobjects.html#//apple_ref/doc/uid/20000948/BAJJBCHI]

----

There seems to be a bug with **General/[NSFont menuFontOfSize:0]**. It returns a font size of 13, but the actual menu font seems to be 14-point.

----

Has anybody noticed a new bug with glyphWithName?  It seems to always return 0 no matter what I pass to it.  a call to numberOfglyphs returns 1745 glyphs (for helvetica) yet absolutely anything I pass to glyphWithName gives me back zero.  Even when I tried passing @"a;lsdkfja;ld" it gave me back zero, and the docs state it should give back -1 if it can't find the glyph you're talking about.  Interestingly enough though, General/NSGlyph is typedefed to an unsigned int, so I'm not quite sure how they plan on returning -1 if they can't find the requested glyph.  Anyway, I always get a box now for every character.  Any one else having this problem?

----

Yes, I've noticed the bug in Tiger with glyphWithName.  I'ts made it damn awkward to get a bezier path of a glyph.  If anyone knows how to map characters in an General/NSString to glyphs of a given font and not call glyphWithName somewhere in the process, I'd very much like to know.  As the previous writer states, an unknown string should return -1 - it doesn't.

See General/NSBezierPathGlyphEncodings. Please don't forget to use the search.