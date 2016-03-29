##前言非常感谢作者提供发资料,这些基本是一些 category 的分类
个人github：https://github.com/xfxfxf

Segment Fault：http://segmentfault.com/a/1190000003520629

（首发在Segment Fault）

当前移动互联网行业太火爆，移动端的需求日益增长，很多开发人员每天都应对着各种需求，作为一名iOS开发人员，对于需求来说，我们要做到的是实现，而对于自己来说，我们需要做到的是写出高质量的代码。

于是，全球的大神们开源了很多高质量、可复用的代码，给予了芸芸众生（心中一万个感谢）。例如我们常用的 AFNetworking，SDWebImage，Masonry 等等，这些第三方库内容强大，性能很高，为大家带来了很多福利。

在开发过程当中，适当合理的使用这些第三方库能帮我们节省很多的时间。这些优秀的第三方库就如同教科书一样，当我们深入挖掘的时候，才能获得更高的提升。

好了，吹了半天牛，我们现在到底要做什么呢？其实我想说的是，合理的使用第三方库能大大的提升开发效率，也许我们自己研究做动画弄半天，还不如开源动画好用，这样的情况很多时候我们是不得不承认的。与其与之较劲，不如我们先使用它们的框架，然后再做深入探究，这样方能更好的掌握。

网上很多好的整理，我这里引用一下：[刚刚在线][1]博客，里面有很多整理好的内容，非常好的干货。感谢原作者的内容，其中有一个整理的是iOS开发好用的 category，能帮我们节省很多精力，接下来我就先一一分析github上面这些category，翻译其中重要的内容。

声明：本人翻译并不能做到百分之百准确，内容如果有误，欢迎下方评论指导，谢谢！

##UIImageView_FaceAwareFill

简介

地址：https://github.com/Julioacarrettoni/UIImageView_FaceAwareFill

This category applies Aspect Fill content mode to an image and if faces are detected it centers them instead of centering the image just by its geometrical center.
这个 category 使用了 Aspect Fill 的模式来显示图片并且当人脸被检测到时，它会就以脸部中心替代图片的集合中心。

使用

pch 文件中直接导入 

```
#import "UIImageView+UIImageView_FaceAwareFill.h"
```
   
设置完一个`UIImageView`的属性以后直接
```
[self.imageView faceAwareFill];
```
    
然后就完了。。。。。

个人评价

看到没有，大神的提供的方法就是如此狂拽炫酷叼霸天，就是如此的简单。


##NSRegularEx+ObjCRegex

简介
地址：https://github.com/bendytree/Objective-C-RegEx-Categories

This project simplifies regular expressions in Objective-C and Swift.
这个猛，直接把`objective-c`和`swift`里面的正则表达式给整合了。

这是一组对比
```
// Without this library
NSString* string = @"I have 2 dogs.";
NSRegularExpression *regex = [NSRegularExpression regular ExpressionWithPattern:@"\\d+" options:NSRegularExpressionCaseInsensitive error:&error];
NSTextCheckingResult *match = [regex firstMatchInString:string options:0 range:NSMakeRange(0, [string length])];
BOOL isMatch = match != nil;

// With this library
BOOL isMatch = [@"I have 2 dogs." isMatch:RX(@"\\d+")];
```
使用

安装过程就不赘述了，要么是cocoapods，要么直接拖进去。

老规矩，在 pch 文件中添加：

```objective-c
#ifdef __OBJC__
    /* ...other references... */
    #import "RegExCategories.h"
#endif
```
当然，你的工程需要开启`ARC`。

`Swift`支持
这个就需要一个桥接文件，百度即可，`Swift`引用 OC 的三方都是需要一个桥接文件。

后面的教程就不翻译了，直接去看代码吧，少年。

个人评价
还在为正则表达式而纠结吗？还在调试正则表达式问题吗？没错，走过路过不要错误，这里有你想要的一切。

##NSObject+AutoCoding

简介

地址：https://github.com/nicklockwood/AutoCoding

这个是一个`NSObject`的 category，提供了对`NSCoding`和`NSCopying`的自动支持。这意味着你不要写`initWithCoder:`和`encodeWithCoder:`了，这个直接承包了。

当然，怎么用还是要看自己的，它并不能读懂你的思维。还有举个例子，你应该避免使用结构体因为它并不遵循`NSCoding`协议，而是通过`NSValue`。

支持很多版本

支持`ARC`和`MRC`

线程安全

使用

直接把`AutoCoding.h`和`AutoCoding.m`拖进工程。

其实自己写归档和反归档也没有那么复杂，这里就不做详细介绍了。

个人评价

这个其实还好，不过其中的机制很不错，值得一看，后面有时间我再翻译。

##UILabel-ContentSize

简介

来源：https://github.com/mergesort/UILabel-ContentSize

使用

通过传入的字符串来改变`UILabel`的`Size`。

直接把`.h`和`.m`文件导入工程吧。

个人评价

正如同作者所说的，总是会忘记操作细节，不如直接写成 category。

##UIViewController-Swizzled

简介

来源：https://github.com/RuiAAPeres/UIViewController-Swizzled

这个能帮你管理你的应用。当你正在做复杂的行为以及刚接手工程的时候这个会变得特别好用。使用这个 category 能看到你现在所在的`UIViewController`，还有展示你进入的层次。

使用

老规矩，要么直接拖入，要么用`cocoapods`。

需要导入链接库：

```
libobjc.dylib
```

然后导入头文件：

```
#import "UIViewController+Swizzled.h"
```

在`AppDelegate`中，你需要在方法`- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions`方法里面加入`SWIZZ_IT `开启。如果因为什么原因你想要停止，只需要添加`UN_SWIZZ_IT `。

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    SWIZZ_IT;
    self.window = [[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
    [self.window makeKeyAndVisible];

    // Your code...

    return YES;
}
```
然后就能看到输出：

```
2013-09-09 18:58:42.360 Testing[25399:c07] -> UINavigationController
2013-09-09 18:58:42.361 Testing[25399:c07] ---> RPViewController
2013-09-09 18:59:55.072 Testing[25399:c07] -----> RPSecondViewController
2013-09-09 18:59:57.367 Testing[25399:c07] -------> RPThirdViewController
2013-09-09 18:59:58.801 Testing[25399:c07] -----> RPSecondViewController
2013-09-09 19:00:00.282 Testing[25399:c07] -------> RPThirdViewController
2013-09-09 19:00:01.906 Testing[25399:c07] ---------> RPViewController
2013-09-09 19:00:03.515 Testing[25399:c07] -------> RPThirdViewController
2013-09-09 19:00:04.267 Testing[25399:c07] -----> RPSecondViewController
2013-09-09 19:00:05.041 Testing[25399:c07] ---> RPViewController
2013-09-09 19:00:07.193 Testing[25399:c07] -----> RPSecondViewController
2013-09-09 19:00:08.312 Testing[25399:c07] -------> RPThirdViewController
2013-09-09 19:00:09.396 Testing[25399:c07] ---------> RPViewController
2013-09-09 19:00:10.183 Testing[25399:c07] -----------> RPSecondViewController
2013-09-09 19:00:10.905 Testing[25399:c07] -------------> RPThirdViewController
2013-09-09 19:00:12.141 Testing[25399:c07] ---------------> RPViewController
2013-09-09 19:00:13.156 Testing[25399:c07] -----------------> RPSecondViewController
```

个人评价

当你刚接手一个新的项目的时候，无数个文件。

这是什么鬼？程序怎么运行的？那个类是干嘛用的？为什么运行到了这里，还有，文件怎么找？要疯掉了。。。

有了此神器，天黑都不怕，一步一步是爪牙，是魔鬼的步伐，程序的运行一清二楚，简直出门旅行，居家必备之良药。

你值得拥有！

##NSDate-Escort

简介

来源：https://github.com/azu/NSDate-Escort

加强`NSDate`

使用

```
/**
 Returns the calendarIdentifier of calendars that is used by this library for date calculation.
 @see AZ_setDefaultCalendarIdentifier: for more details.
 */
+ (NSString *)AZ_defaultCalendarIdentifier;
/**
 Sets the calendarIdentifier of calendars that is used by this library for date calculation.
 You can specify any calendarIdentifiers predefined by NSLocale. If you provide nil, the library uses
 [NSCalendar currentCalendar]. Default value is nil.

 You can't provide individual calendars for individual date objects. If you need to perform such
 complicated date calculations, you should rather create calendars on your own.
 */
+ (void)AZ_setDefaultCalendarIdentifier:(NSString *)calendarIdentifier;

#pragma mark - Relative dates from the current date

- (BOOL)isYesterday;
- (BOOL)isSameWeekAsDate:(NSDate *) aDate;
- (BOOL)isThisWeek;
- (BOOL)isNextWeek;
- (BOOL)isLastWeek;
- (BOOL)isSameMonthAsDate:(NSDate *) aDate;
- (BOOL)isThisMonth;
- (BOOL)isSameYearAsDate:(NSDate *) aDate;
- (BOOL)isThisYear;
- (BOOL)isNextYear;
- (BOOL)isLastYear;
- (BOOL)isEarlierThanDate:(NSDate *) aDate;
- (BOOL)isLaterThanDate:(NSDate *) aDate;
- (BOOL)isEarlierThanOrEqualDate:(NSDate *) aDate;
- (BOOL)isLaterThanOrEqualDate:(NSDate *) aDate;
- (BOOL)isInFuture;
- (BOOL)isInPast;
#pragma mark - Date roles
- (BOOL)isTypicallyWorkday;
- (BOOL)isTypicallyWeekend;
#pragma mark - Adjusting dates
- (NSDate *)dateByAddingYears:(NSInteger) dYears;
- (NSDate *)dateBySubtractingYears:(NSInteger) dYears;
- (NSDate *)dateByAddingMonths:(NSInteger) dMonths;
- (NSDate *)dateBySubtractingMonths:(NSInteger) dMonths;
- (NSDate *)dateByAddingDays:(NSInteger) dDays;
- (NSDate *)dateBySubtractingDays:(NSInteger) dDays;
- (NSDate *)dateByAddingHours:(NSInteger) dHours;
- (NSDate *)dateBySubtractingHours:(NSInteger) dHours;
- (NSDate *)dateByAddingMinutes:(NSInteger) dMinutes;
- (NSDate *)dateBySubtractingMinutes:(NSInteger) dMinutes;
- (NSDate *)dateAtStartOfDay;
- (NSDate *)dateAtEndOfDay;
- (NSDate *)dateAtStartOfWeek;
- (NSDate *)dateAtEndOfWeek;
- (NSDate *)dateAtStartOfMonth;
- (NSDate *)dateAtEndOfMonth;
- (NSDate *)dateAtStartOfYear;
- (NSDate *)dateAtEndOfYear;
#pragma mark - Retrieving intervals
- (NSInteger)minutesAfterDate:(NSDate *) aDate;
- (NSInteger)minutesBeforeDate:(NSDate *) aDate;
- (NSInteger)hoursAfterDate:(NSDate *) aDate;
- (NSInteger)hoursBeforeDate:(NSDate *) aDate;
- (NSInteger)daysAfterDate:(NSDate *) aDate;
- (NSInteger)daysBeforeDate:(NSDate *) aDate;
- (NSInteger)monthsAfterDate:(NSDate *) aDate;
- (NSInteger)monthsBeforeDate:(NSDate *) aDate;
/**
* return distance days
*/
- (NSInteger)distanceInDaysToDate:(NSDate *) aDate;
#pragma mark - Decomposing dates
/**
* return nearest hour
*/
@property(readonly) NSInteger nearestHour;
@property(readonly) NSInteger hour;
@property(readonly) NSInteger minute;
@property(readonly) NSInteger seconds;
@property(readonly) NSInteger day;
@property(readonly) NSInteger month;
@property(readonly) NSInteger week;
//  in the Gregorian calendar, n is 7 and Sunday is represented by 1.
@property(readonly) NSInteger weekday;
@property(readonly) NSInteger firstDayOfWeekday;
@property(readonly) NSInteger lastDayOfWeekday;
// e.g. 2nd Tuesday of the month == 2
@property(readonly) NSInteger nthWeekday;
```

个人评价

无需多说，看方法名字就知道有什么作用了，回想起之前处理时间的日子。。。多么痛的领悟，果然那句话很对：磨刀不误砍柴工。

##UIView+Toast

简介

来源：https://github.com/scalessec/Toast

使用

注意导入`QuartzCore `

图片已经实例代码源地址都有，就几个参数

- `makeToast`    要显示的内容
- `duration`    持续时间
- `position`    放置的位置
- `title`    标题
- `image`    放置的图片
- `makeToastActivity`    显示 toast    

个人评价

简单好用，清晰明了。

##NYXImagesKit

简介

来源：https://github.com/Nyx0uf/NYXImagesKit

NYXImagesKit是一个重组了多个有用的UIImage categories的iOS项目，可对图像/图片进行多个处理，比如筛选、模糊、优化、蒙版、调整大小、旋转以及保存等等。同时还提供了一个UIImageView子类从URL异步加载图片，并在下载完毕时展示图片。

使用

首先打开`NYXImagesKit.xcodeproj`然后运行库，之后把库和头文件导入到你的工程里面，最后要链接以下的框架：

- Accelerate
- AssetsLibrary
- ImageIO
- MobileCoreServices
- QuartzCore
- CoreImage

**UIImage+Blurring**
模糊效果
```
[myImage gaussianBlurWithBias:0];
```
**UIImage+Masking**
蒙板效果
```
UIImage* masked = [myImage maskWithImage:[UIImage imageNamed:@"mask.png"]];
```
**UIImage+Resizing**
重置尺寸

1. 上左
2. 上中
3. 上右
4. 下左
5. 下中
6. 下右
7. 左中
8. 右中
9. 中间

```objective-c
UIImage* cropped = [myImage cropToSize:(CGSize){width, height} usingMode:NYXCropModeCenter];
```
`NYXCropMode`是一个枚举类型，能在头文件里面找到，表示不同的类型

**Scaling**
缩放

你有两种方法来缩放图片，这两种方法都能保持原图片比例

```objective-c
UIImage* scaled1 = [myImage scaleByFactor:0.5f];
UIImage* scaled2 = [myImage scaleToFitSize:(CGSize){width, height}];
```

**UIImage+Rotating**
旋转

```
UIImage* rotated1 = [myImage rotateInDegrees:217.0f];
UIImage* rotated2 = [myImage rotateInRadians:M_PI_2];
UIImage* flipped1 = [myImage verticalFlip];
UIImage* flipped2 = [myImage horizontalFlip];
```

**UIImage+Reflection**
重构图片
```
UIImage* reflected = [myImage reflectedImageWithHeight:myImage.size.height fromAlpha:0.0f toAlpha:0.5f];
```

**UIImage+Enhancing**
提升

```
[myImage autoEnhance];
[myImage redEyeCorrection];
```

**UIImage+Saving**
保存类型

这个能把图片存到一个地址或者相册，支持五种类型

1. BMP
2. GIF
3. JPG 
4. PNG
5. TIFF

要用这个就必须导入`ImageIO.framework`，`MobileCoreServices.framework`还有`AssertsLibrary.framework`。

```
[myImage saveToURL:url type:NYXImageTypeJPEG backgroundFillColor:nil];
[myImage saveToPath:path type:NYXImageTypeTIFF backgroundFillColor:[UIColor yellowColor]];
[myImage saveToPhotosAlbum];
```

**NYXProgressiveImageView**

这个是继承`UIImageView`的一个类，能异步加载图片和缓存。

当然，我们可以使用`SDWebImage`。

**个人评价**

这个针对于图片处理，很好很强大。

##MJPopupViewController

简介

来源：https://github.com/martinjuhasz/MJPopupViewController

这个是给`UIViewController`提供过渡效果的。

使用

把`Source`目录下的文件夹拖入工程，然后导入`QuartzCore.framework`。

引入文件
```
#import "UIViewController+MJPopupViewController.h"
```

简单添加

```
[self presentPopupViewController:detailViewController animationType:MJPopupViewAnimationFade];
```

如果要消失

```
[self dismissPopupViewControllerWithanimationType:MJPopupViewAnimationFade];
```

在实例工程中可以看到更多的使用方法。

个人评价

一个非常简单容易使用的过渡效果，有需求的时候可以使用。

##UIColor+Colours

简介

来源：https://github.com/bennyguitar/Colours

为`UIColor`提供更多颜色支持

使用

`cocoapods`安装，或者拖入文件

颜色过多，就不一一列举了。

**RGBA**

通过数组可以取出`UIColor`的四个参数，都是`NSNumber`类型，记得他们都是0-1的数，不是0-255

```
NSArray *colorArray = [[UIColor seafoamColor] rgbaArray];
UIColor *newColor = [UIColor colorFromRGBAArray:colorArray];
```

字典也能取到值

- kColoursRGBA_R
- kColoursRGBA_G
- kColoursRGBA_B
- kColoursRGBA_A

```objective-c
NSDictionary *colorDict = [[UIColor seafoamColor] rgbaDictionary];
UIColor *newColor = [UIColor colorFromRGBADictionary:colorDict];

// You can also get a single component like so:
NSNumber *r = colorDict[kColoursRGBA_R];
```

后面还有很多方法，不一一列举了。

个人评价

实际开发中，一般 UI 设计出来各种颜色，位置都确定了，所以不好说这个用的多不多。

##NSDate+Helper

简介

来源：https://github.com/billymeltdown/nsdate-helper

这也是一个扩展`NSDate`的 category

使用

使用方便，`stringForDisplayFromDate`能非常便捷的显示出很多信息。

```objective-c
NSString *displayString = [NSDate stringForDisplayFromDate:date];
```

这能显示出很多信息

- ‘3:42 AM’ – 如果时间是在今天半夜
- ‘Tuesday’ – 如果时间是在这个星期
- ‘Mar 1’ – 如果日期是在今年
- ‘Mar 1, 2008’ – else ;-)

另外的方法能显示几天之前这样的信息

```objective-c
NSDate *date = [NSDate date];
  [date daysAgo]; // provides an NSComponent-based NSUInteger describing days ago.
  [date daysAgoAgainstMidnight]; // better version of daysAgo, works off midnight (hat-tip: "sburlot":http://github.com/sburlot)
  [date stringDaysAgo]; // 'Today', 'Yesterday', or 'N days ago'.
```

构造`date formatters`很纠结？缺少`to_s(:db)`？我也是，`NSDate (Helper)`有些静态方法能够在两者之间转换，而且能支持数据库的时间戳。

```objective-c
NSDate *date = [NSDate dateFromString:@"2009-03-01 12:15:23"];
NSString *dbDateString = [NSDate stringFromDate:date]; // returns '2009-03-01 12:15:23'
```
还有

```objective-c
NSString *otherDateString = [NSDate stringFromDate:date withFormat:@"EEEE"]; // use any format you like
```

个人评价

这个也不错，更多功能可以在`.h`文件里面找，命名很规范。


##ObjectiveSugar

简介

来源：https://github.com/supermarin/ObjectiveSugar

语法糖功能

使用

使用`cocoapods`，然后导入头文件`#import <ObjectiveSugar/ObjectiveSugar.h>`

`NSNumber`

```objective-c
[@3 times:^{
    NSLog(@"Hello!");
}];
// Hello!
// Hello!
// Hello!

[@3 timesWithIndex:^(NSUInteger index) {
    NSLog(@"Another version with number: %d", index);
}];
// Another version with number: 0
// Another version with number: 1
// Another version with number: 2


[@1 upto:4 do:^(NSInteger numbah) {
    NSLog(@"Current number.. %d", numbah);
}];
// Current number.. 1
// Current number.. 2
// Current number.. 3
// Current number.. 4

[@7 downto:4 do:^(NSInteger numbah) {
    NSLog(@"Current number.. %d", numbah);
}];
// Current number.. 7
// Current number.. 6
// Current number.. 5
// Current number.. 4

NSDate *firstOfDecember = [NSDate date]; // let's pretend it's 1st of December

NSDate *firstOfNovember = [@30.days since:firstOfDecember];
// 2012-11-01 00:00:00 +0000

NSDate *christmas = [@7.days until:newYearsDay];
// 2012-12-25 00:00:00 +0000

NSDate *future = @24.days.fromNow;
// 2012-12-25 20:49:05 +0000

NSDate *past = @1.month.ago;
// 2012-11-01 20:50:28 +00:00
```

`NSArray / NSSet`

```objective-c
// All of these methods return a modified copy of the array.
// They're not modifying the source array.

NSArray *cars = @[@"Testarossa", @"F50", @"F458 Italia"]; // or NSSet

[cars each:^(id object) {
    NSLog(@"Car: %@", object);
}];
// Car: Testarossa
// Car: F50
// Car: F458 Italia

[cars eachWithIndex:^(id object, NSUInteger index) {
    NSLog(@"Car: %@ index: %i", object, index);
}];
// Car: Testarossa index: 0
// Car: F50 index: 1
// Car: F458 Italia index: 2

[cars each:^(id object) {
    NSLog(@"Car: %@", object);
} options:NSEnumerationReverse];
// Car: F458 Italia
// Car: F50
// Car: Testarossa

[cars eachWithIndex:^(id object, NSUInteger index) {
    NSLog(@"Car: %@ index: %i", object, index);
} options:NSEnumerationReverse];
// Car: F458 Italia index: 2
// Car: F50 index: 1
// Car: Testarossa index: 0

[cars map:^(NSString* car) {
    return car.lowercaseString;
}];
// testarossa, f50, f458 italia

// Or, a more common example:
[cars map:^(NSString* carName) {
    return [[Car alloc] initWithName:carName];
}];
// array of Car objects

NSArray *mixedData = @[ @1, @"Objective Sugar!", @"Github", @4, @"5"];

[mixedData select:^BOOL(id object) {
  return ([object class] == [NSString class]);
}];
// Objective Sugar, Github, 5

[mixedData reject:^BOOL(id object) {
    return ([object class] == [NSString class]);
}];
// 1, 4

NSArray *numbers = @[ @5, @2, @7, @1 ];
[numbers sort];
// 1, 2, 5, 7

cars.sample
// 458 Italia
cars.sample
// F50
```

`NSArray`only

```objective-c
NSArray *numbers = @[@1, @2, @3, @4, @5, @6];

// index from 2 to 4
numbers[@"2..4"];
// [@3, @4, @5]

// index from 2 to 4 (excluded)
numbers[@"2...4"];
// [@3, @4]

// With NSRange location: 2, length: 4
numbers[@"2,4"];
// [@3, @4, @5, @6]

NSValue *range = [NSValue valueWithRange:NSMakeRange(2, 4)];
numbers[range];
// [@3, @4, @5, @6]

[numbers reverse];
// [@6, @5, @4, @3, @2, @1]


NSArray *fruits = @[ @"banana", @"mango", @"apple", @"pear" ];

[fruits includes:@"apple"];
// YES

[fruits take:3];
// banana, mango, apple

[fruits takeWhile:^BOOL(id fruit) {
    return ![fruit isEqualToString:@"apple"];
}];
// banana, mango

NSArray *nestedArray = @[ @[ @1, @2, @3 ], @[ @4, @5, @6, @[ @7, @8 ] ], @9, @10 ];
[nestedArray flatten];
// 1, 2, 3, 4, 5, 6, 7, 8, 9, 10

NSArray *abc = @[ @"a", @"b", @"c" ];
[abc join];
// abc

[abc join:@"-"];
// a-b-c

NSArray *mixedData = @[ @1, @"Objective Sugar!", @"Github", @4, @"5"];

[mixedData detect:^BOOL(id object) {
    return ([object class] == [NSString class]);
}];
// Objective Sugar



// TODO: Make a better / simpler example of this
NSArray *landlockedCountries = @[ @"Bolivia", @"Paraguay", @"Austria", @"Switzerland", @"Hungary" ];
NSArray *europeanCountries = @[ @"France", @"Germany", @"Austria", @"Spain", @"Hungary", @"Poland", @"Switzerland" ];


[landlockedCountries intersectionWithArray:europeanCountries];
// landlockedEuropeanCountries = Austria, Switzerland, Hungary

[landlockedCountries unionWithArray:europeanCountries];
// landlockedOrEuropean = Bolivia, Paraguay, Austria, Switzerland, Hungary, France, Germany, Spain, Poland

[landlockedCountries relativeComplement:europeanCountries];
// nonEuropeanLandlockedCountries = Bolivia, Paraguay

[europeanCountries relativeComplement:landlockedCountries];
// notLandlockedEuropeanCountries = France, Germany, Spain, Poland

[landlockedCountries symmetricDifference:europeanCountries];
// uniqueCountries = Bolivia, Paraguay, France, Germany, Spain, Poland
```

`NSMutableArray`

```objective-c
NSMutableArray *people = @[ @"Alice", @"Benjamin", @"Christopher" ];

[people push:@"Daniel"]; // Alice, Benjamin, Christopher, Daniel

[people pop]; // Daniel
// people = Alice, Benjamin, Christopher

[people pop:2]; // Benjamin, Christopher
// people = Alice

[people concat:@[ @"Evan", @"Frank", @"Gavin" ]];
// people = Alice, Evan, Frank, Gavin

[people keepIf:^BOOL(id object) {
    return [object characterAtIndex:0] == 'E';
}];
// people = Evan
```

`NSDictionary`

```objective-c
NSDictionary *dict = @{ @"one" : @1, @"two" : @2, @"three" : @3 };

[dict each:^(id key, id value){
    NSLog(@"Key: %@, Value: %@", key, value);
}];
// Key: one, Value: 1
// Key: two, Value: 2
// Key: three, Value: 3

[dict eachKey:^(id key) {
    NSLog(@"Key: %@", key);
}];
// Key: one
// Key: two
// Key: three

[dict eachValue:^(id value) {
    NSLog(@"Value: %@", value);
}];
// Value: 1
// Value: 2
// Value: 3

NSDictionary *errors = @{
    @"username" : @[ @"already taken" ],
    @"password" : @[ @"is too short (minimum is 8 characters)", @"not complex enough" ],
    @"email" : @[ @"can't be blank" ];
};

[errors map:^(id attribute, id reasons) {
    return NSStringWithFormat(@"%@ %@", attribute, [reasons join:@", "]);
}];
// username already taken
// password is too short (minimum is 8 characters), not complex enough
// email can't be blank

[errors hasKey:@"email"]
// true
[errors hasKey:@"Alcatraz"]
// false
```

`NSString`

```objective-c
NSString *sentence = NSStringWithFormat(@"This is a text-with-argument %@", @1234);
// This is a text-with-argument 1234

[sentence split];
// array = this, is, a, text-with-argument, 1234

[sentence split:@"-"]
// array = this is a text, with, argument 1234

[sentence containsString:@"this is a"];
// YES
```

`C`

```
unless(_messages) {
    // The body is only executed if the condition is false
    _messages = [self initializeMessages];
}

int iterations = 10;
until(iterations == 0) {
    // The body is executed until the condition is false
    // 10 9 8 7 6 5 4 3 2 1
    printf("%d ", iterations);
    iterations--;
}
printf("\n");

iterations = 10;
do {
    // The body is executed at least once until the condition is false
    // Will print: Executed!
    printf("Executed!\n");
} until(true);
```

个人评价

这是什么黑科技，简直改变 OC 语法，简化更多语法，简直停不下来。

##Kiwi

简介

来源：https://github.com/kiwi-bdd/Kiwi

Kiwi的作用是用来过来更方便的测试程序，可读性更高。

使用

```
pod "Kiwi"
```

详细需要看文档。

个人评价

又是一个黑科技，用的时候再查看文档吧。

##ViewUtils

简介

来源：https://github.com/nicklockwood/ViewUtils

**目的**
扩展`UIView`的 category，有几个方面：

- 载入`Nib`- 不需要`UIViewController`就能载入视图
- 布局 - 能独立设置位置或者宽/高
- 搜索 - 检索子视图，通过类，tag 或者正则表达式
- 响应者 - 找到一个 view 的第一响应者

**线程安全**
这个只能在主线程使用

使用

把两个文件拖入工程

方法封装了系统的`UIView`，很多都是非常实用且增加了安全性能。

还能单独修改`frame`的值。

个人评价
封装`UIView`的通用功能，安全性得到提高，还能单独修改`frame`，增加了很多便利。

##NSDate-TimeAgo

简介

来源：https://github.com/kevinlawler/NSDate-TimeAgo

可以显示当前时间是多久以前，不过这个已经并入了另一个库里面

使用

导入`#import "NSDate+TimeAgo.h"`
```objective-c
NSDate *date = [[NSDate alloc] initWithTimeIntervalSince1970:0];
NSString *ago = [date timeAgo];
NSLog(@"Output is: \"%@\"", ago);
2011-11-12 17:19:25.608 Proj[0:0] Output is: "41 years ago"
```

还有两种方法

- dateTimeAgo - 返回`{value} {unit} ago `这种格式
- dateTimeUntilNow - 返回`昨天/今早/上个星期/这个月`，没有上面的精确但是更自然。

个人评价

如果只需要很简单的功能，这个就能满足，如果需要对时间更强大处理

访问：https://github.com/MatthewYork/DateTools

##iOS-FontAwesome

简介

来源：https://github.com/alexdrone/ios-fontawesome

添加字体，还有图片

使用

首先，在工程里面必须有`FontAwesome.ttf`，而且在`plist`文件中的`UIAppFonts`必须包换一个`String item`名字叫`FontAwesome.ttf`

然后再导入`NSString+FontAwesome`

```objective-c
UILabel *label = [...]
label.font = [UIFont fontWithName:kFontAwesomeFamilyName size:20];
```
还能使用枚举

```objective-c
label.text = [NSString fontAwesomeIconStringForEnum:FAGithub];
```
当然，最重要还是查看文档，里面提供各种字体。

个人评价

确实很不错，很多种类型的字体，还有图片的，总之很给力。

##NSObject-AutoDescription

简介

来源：https://github.com/djmadcat/NSObject-AutoDescription

增加对`NSArray`，`NSDictionary`还有`NSSet`的描述支持

使用
```objective-c
#import "NAUser.h"
#import "NSObject+AutoDescription.h"

@implementation NAUser

- (NSString *)description
{
    return [self autoDescription];
}

@end
```

个人评价

小而美，有需求的话可以用下。

##CGRectPositioning

简介

来源:https://github.com/mvx24/CGRectPositioning

这个是个宏文件

可以对`CGRect`很方便的处理

使用

看名字就能知道了，把`CGRectPositioning.h`导入工程，里面全是宏

个人评价

代码布局的时候，使用这个就能很方便





##总结

先从学习使用开始，到研究分析如何实现，才是大智慧。


  [1]: http://www.superqq.com/blog/2015/01/15/objective-cxiang-guan-categoryde-shou-ji/
