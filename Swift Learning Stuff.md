
# 1. OBJECTIVE C CODING STANDARDS

## 1.1 File Organization

The physical files should be kept in sync with the Xcode project files
Any Xcode groups created should be reflected by folders in the filesystem
Code should be grouped not only by type, but also by feature for greater clarity.

## 1.2 Code Organization

Use #pragma mark - to categorize methods in functional groupings and protocol/delegate implementations following this general structure.

```objective-c
#pragma mark - Lifecycle

- (instancetype)init {}
- (void)dealloc {}
- (void)viewDidLoad {}
- (void)viewWillAppear:(BOOL)animated {}
- (void)didReceiveMemoryWarning {}
``` 

```objective-c
#pragma mark - Custom Accessors

- (void)setCustomProperty:(id)value {}
- (id)customProperty {}
```
```objective-c
#pragma mark - IBActions

- (IBAction)submitData:(id)sender {}
```
```objective-c
#pragma mark - Public

- (void)publicMethod {}
```

```objective-c
#pragma mark - Private

- (void)privateMethod {}
```
```
#pragma mark - Protocol conformance
#pragma mark - UITextFieldDelegate
#pragma mark - UITableViewDataSource
#pragma mark - UITableViewDelegate
```

```objective-c
#pragma mark - NSCopying

- (id)copyWithZone:(NSZone *)zone {}
```
```objective-c
#pragma mark - NSObject
- (NSString *)description {}
```

If there is more than one import statement, group the statements together. Commenting each group is optional.
For modules use the @import syntax.

Example :

```objective-c
// Frameworks
@import QuartzCore;

// Models
#import "NYTUser.h"

// Views
#import "NYTButton.h"
#import "NYTUserView.h"
```

## 1.3 Spacing

* Indent using 4 spaces. Never indent with tabs. Be sure to set this preference in Xcode.

* Method braces and other braces (if/else/switch/while etc.) always open on the same line as the statement but close on a new line.

* There should be exactly one blank line between methods to aid in visual clarity and organization.

* Whitespace within methods should be used to separate functionality (though often this can indicate an opportunity to split the method into several, smaller methods). In methods with long or verbose names, a single line of whitespace may be used to provide visual separation before the method’s body.

* @synthesize and @dynamic should each be declared on new lines in the implementation.

* Use Uncrustify Xcode plugin for standard code spacing

Preferred :

```objective-c
if (user.isHappy) {
  //Do something
} else {
  //Do something else
}
```

Not Preferred :

```objective-c
if (user.isHappy)
{
    //Do something
}
else {
    //Do something else
}
```

## 1.4 Commenting

When they are needed, comments should be used to explain why a particular piece of code does something. Any comments that are used must be kept up-to-date or deleted.


## 1.5 Documentation

* Objective-C documentation is designated by a /** */ comment block (note the extra initial star), which precedes any @interface or @protocol, as well as any method or @property declarations.

* For classes, categories, and protocols, documentation should describe the purpose of that particular component, offering suggestions and guidelines for how it should be used.
 
* Always document that how a class should (or should not) be subclassed, or any caveats in behavior for standard protocols (like NSCopying) should always be documented.

### Major Commands used for commenting 

* @file: Use this tag to indicate that you’re documenting a file (header or not). If you’re about to use Doxygen to produce documentation, then you’d better set the file name right after this tag. It’s a top level tag.
* @header: Similar to the above, but used with HeaderDoc. Don’t use the above if you won’t use Doxygen.
* @author Use it to write the author info of the file.
* @copyright: Add copyright info.
* @version: Use it to write the current version of the file. Pretty important if versioning matters during the project’s lifetime.
* @brief: Use it to write a short description about the method, property, class, file, struct, or enum you’re documenting. No line breaks are allowed.
* @discussion: Use it to write a thorough description. You can add line breaks if needed.
* @param: With this you can describe a parameter of a method or function. You can have multiple such tags.
* @return: Use it to specify the return value of a method or function.
* @see: Use it to indicate other related method or functions. You can have multiple such tags.
* @code: With this tag, you can embed code snippets in the documentation. When viewing the documentation in Help Inspector, the code is represented with a different font, inside a special box. Always use the @endcode tag when you finish writing code.
* @remark: Use it to highlight any special facts about the code you’re currently documenting

#### Example :

File Name Commenting

```objective-c
/**
@header ViewController.h
 
@brief This is the header file where my super-code is contained.
 
This file contains the most importnant method and properties decalaration. It's parted by two methods in total, which can be used to perform temperature conversions.
 
@author Your_Name
@copyright  2015 Your_Name
@version    15.12.7
*/
```

 Method Name Commenting

```objective-c
/**
    @brief It converts temperature degrees from Fahrenheit to Celsius scale.
 
    @discussion This method accepts a float value representing the temperature in <b>Fahrenheit</b> scale and it converts it to the <i>Celsius</i> scale.
 
                To use it, simply call @c[self toCelsius: 50];
 
    @param  fromFahrenheit The input value representing the degrees in the Fahrenheit scale.
 
    @return float The degrees in the Celsius scale.
*/
-(float)toCelcius:(float)fromFahrenheit;
```

* Documentation required for the header files. However this doesn’t mean that description to implementation files should not be added.

* Make sure you don’t leave any part undocumented. Since, implementation is not shown in exported documentation, but the description of all files is always visible.

* Use VVDocumenter xcode plugin to create the commenting for the documentation automatically 

## 1.6. Naming Conventions

Naming Convention plays very important role while writing up the code. Major Points to remember

* Be clear and brief while naming classes, objects, variables etc.

Preferred :- 

``` objective-c
insertObject:atIndex:
removeObjectAtIndex:
removeObject:
```

Not Preferred :- 

``` objective-c
insert:at:
remove:
```

* Long, descriptive method and variable names are good.

Preferred :- 

``` objective-c
UIButton *settingsButton;
```

Not Preferred :-

``` objective-c
UIButton *setBut;
```

* Use names consistently throughout the Objective C programming

* Methods that do the same thing in different classes should have the same name

## 1.7. PREFIXES - Project Initials or ZBT 

* All classes in an Objective-C application must be globally unique. Since many different frameworks are likely have some conceptual overlap—and therefore an overlap in names (users, views, requests / responses, etc.)—convention dictates that class names use 2 or 3 letter prefix.

* Apple recommends that 2-letter prefixes be reserved for first-party libraries and frameworks, while third-party developers (that's us) opt for 3 letters or more
We will be using Project Initials for the respective project or (Zapbuild Technologies) as prefix if creating any framework or reusable component

* Constants should be camel-case with all words capitalized and prefixed by the related class name for clarity.

* Avoid the use of the underscore character as a prefix meaning private in method names

Preferred :- 

``` objective-c
ZBTLoginViewController
ZBTRegisterViewController
ZBTUserModel
ZBTConstantBaseURL
static NSTimeInterval const ZBTLoginViewControllerNavigationFadeAnimationDuration = 0.3;
````

Not Preferred :-

``` objective-c
LoginVC
RegisterVC
UserModel
kBaseURL
static NSTimeInterval const fadetime = 1.7;
```

* Use prefixes when naming 
a) Classes
b) Protocols
c) Constants
d) Typedef structures
e) Methods (only for Categories and Swizzling)

* Don’t Use prefixes when naming
a) Methods (except Categories and Swizzling)

* For methods, constants and variables -> first letter should be small 

* For classes -> first letter should be Capital


## 1.8. Naming Methods Conventions 

* For methods that represent actions an object takes, start the name with a verb

* Do not use “do” or “does” as part of the name because these auxiliary verbs rarely add meaning. Also, never use adverbs or adjectives before the verb

* Use keywords before all arguments

Preferred :-

``` objective-c
- (void)sendAction:(SEL)aSelector toObject:(id)anObject forAllCells:(BOOL)flag;
```

Not Preferred :-

``` objective-c
- (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag;
```

* Make the word before the argument describe the argument

Preferred :-

``` objective-c
- (id)viewWithTag:(NSInteger)aTag;
```

Not Preferred :- 

``` objective-c
- (id)taggedView:(int)aTag;
```

* Don’t use “and” to link keywords that are attributes of the receiver.

Preferred :-

``` objective-c
- (int)runModalForDirectory:(NSString *)path file:(NSString *) name types:(NSArray *)fileTypes;
```

Not Preferred :-

``` objective-c
- (id)taggedView:(int)aTag;
```

* If the method describes two separate actions, use “and” to link them.

Example :-

``` objective-c
- (BOOL)openFile:(NSString *)fullPath withApplication:(NSString *)appName andDeactivate:(BOOL)flag;
```

## 1.9 Accessor Methods

* Accessor methods are those methods that set and return the value of a property of an object. They have certain recommended forms, depending on how the property is expressed

* Noun :- 
```
- (type)noun;
- (void)setNoun:(type)aNoun;
```

Example :-
```	
	- (NSString *)title;
	- (void)setTitle:(NSString *)aTitle;
```

* Adjective :- 
```	
  - (BOOL) isAdjective;
	- (void) setAdjective:(BOOL)flag;
```

Example :-
```
	- (BOOL) isEditable;
	- (void) setEditable:(BOOL)flag;
```

* Verb :- 
```	
  - (BOOL) verbObject;
	- (void) setVerbObject:(type)flag;
```

Example :-
```	
  - (BOOL)showsAlpha;
	- (void)setShowsAlpha:(BOOL)flag;
```
* The verb should be in the simple present tense.

* Don’t twist a verb into an adjective by using a participle:

* Preferred :-

``` objective-c
- (void)setAcceptsGlyphInfo:(BOOL)flag;
- (BOOL)acceptsGlyphInfo;
```

Not Preferred :- 

``` objective-c
- (void)setGlyphInfoAccepted:(BOOL)flag;
- (BOOL)glyphInfoAccepted;
```

* Use “get” only for methods that return objects and values indirectly. You should use this form for methods only when multiple items need to be returned.

Example :-

``` objective-c
- (void)getLineDash:(float *)pattern count:(int *)count phase:(float *)phase;
```

## 1.10. Delegate Methods

* Start the name by identifying the class of the object that’s sending the message:

Example :-

``` objective-c
- (BOOL)tableView:(NSTableView *)tableView shouldSelectRow:(int)row;
- (BOOL)application:(NSApplication *)sender openFile:(NSString *)filename;
```

* Use “did” or “will” for methods that are invoked to notify the delegate that something has happened or is about to happen.

Example :-

``` objective-c
- (void)browserDidScroll:(NSBrowser *)sender;
```


## 1.11. Method Arguments

* As with methods, arguments start with a lowercase letter and the first letter of successive words are capitalized (for example, removeObject:(id)anObject).

* Don’t use “pointer” or “ptr” in the name. Let the argument’s type rather than its name declare whether it’s a pointer.

* Avoid one- and two-letter names for arguments.
* Avoid abbreviations that save only a few letters.


## 1.12. Variables

* Variables should be named as descriptively as possible. Single letter variable names should be avoided except in for() loops.

* Asterisks indicating pointers belong with the variable, e.g., NSString *text not NSString* text orNSString * text, except in the case of constants.

* Private properties should be used in place of instance variables whenever possible. Although using instance variables is a valid way of doing things, by agreeing to prefer properties our code will be more consistent.

Preferred -

``` objective-c
@interface RWTTutorial : NSObject

@property (strong, nonatomic) NSString *tutorialName;

@end
```

``` objective-c
Not Preferred -

@interface RWTTutorial : NSObject {
  NSString *tutorialName;
}
````

Example -

``` objective-c
NSString *title: It is reasonable to assume a “title” is a string.
NSString *titleHTML: This indicates a title that may contain HTML which needs parsing for display. “HTML” is needed for a programmer to use this variable effectively.
NSAttributedString *titleAttributedString: A title, already formatted for display.AttributedString hints that this value is not just a vanilla title, and adding it could be a reasonable choice depending on context.
NSDate *now: No further clarification is needed.
NSDate *lastModifiedDate: Simply lastModified can be ambiguous; depending on context, one could reasonably assume it is one of a few different types.
NSURL *URL vs. NSString *URLString: In situations when a value can reasonably be represented by different classes, it is often useful to disambiguate in the variable’s name.
NSString *releaseDateString: Another example where a value could be represented by another class, and the name can help disambiguate.
```

## 1.13. Private Properties

* Private properties should be declared in class extensions (anonymous categories) in the implementation file of a class

For example:

``` objective-c
@interface ZBTAdvertisement ()

@property (nonatomic, strong) GADBannerView *googleAdView;
@property (nonatomic, strong) ADBannerView *iAdView;
@property (nonatomic, strong) UIWebView *adXWebView;

@end
```

## 1.14. Literals

* NSString, NSDictionary, NSArray, and NSNumber literals should be used whenever creating immutable instances of those objects. Pay special care that nil values not be passed into NSArrayand NSDictionary literals, as this will cause a crash.

Preferred:

``` objective-c 
NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];
NSDictionary *productManagers = @{@"iPhone": @"Kate", @"iPad": @"Kamal", @"Mobile Web": @"Bill"};
NSNumber *shouldUseLiterals = @YES;
NSNumber *buildingStreetNumber = @10018;
```

Not Preferred:

``` objective-c
NSArray *names = [NSArray arrayWithObjects:@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul", nil];
NSDictionary *productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil];
NSNumber *shouldUseLiterals = [NSNumber numberWithBool:YES];
NSNumber *buildingStreetNumber = [NSNumber numberWithInteger:10018];
```
## 1.15. Constants

* Constants are preferred over in-line string literals or numbers, as they allow for easy reproduction of commonly used variables and can be quickly changed without the need for find and replace. Constants should be declared as static constants and not #defines unless explicitly being used as a macro.

Preferred:

``` objective-c
static NSString * const ZBTAboutViewControllerCompanyName = @"Zapbuild";

static CGFloat const ZBTImageThumbnailHeight = 50.0;
```

Not Preferred:

``` objective-c
#define CompanyName @"Zapbuild"

#define thumbnailHeight 2
```




## 1.16. Enumerated Types & Bitmasks

* Use NS_Enum only and not enum or older k-style constant definitions
* Use NS_Options only for bitmasks
* Include Prefix for the Enums and the name of enum should be present in the enum type values

For Example:

``` objective-c
typedef NS_ENUM(NSInteger, ZBTLeftMenuTopItemType) {
  ZBTLeftMenuTopItemMain,
  ZBTLeftMenuTopItemShows,
  ZBTLeftMenuTopItemSchedule
};
```

Example:

``` objective-c
typedef NS_OPTIONS(NSUInteger, NYTAdCategory) {
  NYTAdCategoryAutos      = 1 << 0,
  NYTAdCategoryJobs       = 1 << 1,
  NYTAdCategoryRealState  = 1 << 2,
  NYTAdCategoryTechnology = 1 << 3
};
```





## 1.17 Booleans

* Objective-C uses YES and NO. Therefore true and false should only be used for CoreFoundation, C or C++ code.
Since nil resolves to NO it is unnecessary to compare it in conditions.
* Never compare something directly to YES, because YES is defined to 1 and a BOOL can be up to 8 bits.
* If the name of a BOOL property is expressed as an adjective, the property can omit the “is” prefix but specifies the conventional name for the get accessor, for example:

Preferred:

``` objective-c
if (someObject) {}
if (![anotherObject boolValue]) {}
```
Not Preferred:

``` objective-c
if (someObject == nil) {}
if ([anotherObject boolValue] == NO) {}
if (isAwesome == YES) {} // Never do this.
if (isAwesome == true) {} // Never do this.
```

## 1.18. Golden Path
* When coding with conditionals, the left hand margin of the code should be the "golden" or "happy" path. That is, don't nest if statements. Multiple return statements are OK.

Preferred:

``` objective-c
- (void)someMethod {
  if (![someOther boolValue]) {
    return;
  }

  //Do something important
}
```

Not Preferred:

``` objective-c
- (void)someMethod {
  if ([someOther boolValue]) {
    //Do something important
  }
}
```


## 1.19. Error Handling
* When methods return an error parameter by reference, switch on the returned value, not the error variable.

For example:

``` objective-c
NSError *error;
if (![self trySomethingWithError:&error]) {
    // Handle Error
}
```

Not:

``` objective-c
NSError *error;
[self trySomethingWithError:&error];
if (error) {
    // Handle Error
}
```

* Some of Apple’s APIs write garbage values to the error parameter (if non-NULL) in successful cases, so switching on the error can cause false negatives (and subsequently crash).


## 1.20. CGRect Functions

* When accessing the x, y, width, or height of a CGRect, always use the CGGeometry functionsinstead of direct struct member access. From Apple's CGGeometry reference:
* All functions described in this reference that take CGRect data structures as inputs implicitly standardize those rectangles before calculating their results. For this reason, your applications should avoid directly reading and writing the data stored in the CGRect data structure. Instead, use the functions described here to manipulate rectangles and to retrieve their characteristics.

Preferred :

``` objective-c
CGRect frame = self.view.frame;

CGFloat x = CGRectGetMinX(frame);
CGFloat y = CGRectGetMinY(frame);
CGFloat width = CGRectGetWidth(frame);
CGFloat height = CGRectGetHeight(frame);
```

Not Preferred :

``` objective-c
CGRect frame = self.view.frame;

CGFloat x = frame.origin.x;
CGFloat y = frame.origin.y;
CGFloat width = frame.size.width;
CGFloat height = frame.size.height;
```

## 1.21. Categories 
* Categories may be used to concisely segment functionality and should be named to describe that functionality.

For example:

``` objective-c
@interface UIViewController (NYTMediaPlaying)
@interface NSString (NSStringEncodingDetection)
```

Not:

``` objective-c
@interface NYTAdvertisement (private)
@interface NSString (NYTAdditions)
```
