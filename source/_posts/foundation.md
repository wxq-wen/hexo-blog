title: foundation
date: 2015-02-01 16:36:12
tags: Foundation
---

# NSString/NSMutableString

\#include <string.h>

int main(int argc, const char * argv[])
{
    
    /************************  结构体   *********************/
    
    //表示范围 NSRange 表示事物的范围，通常是字符串里的字符范围或者数组里的元素范围
	//    typedef struct _NSRange
	//    {
	//        unsigned int location;//范围起始位置
	//        unsigned int length;//范围内所含元素的个数
	//    } NSRange;
    
    //创建三种方法
    
    //第一种 直接给字段赋值
    NSRange range1;
    range1.location =17;//用NSNotFound表示没有范围
    range1.length =4;
    
    //第二种 应用C语言的聚合结构赋值机制
    NSRange range2= {17,4};
    
    //第三种 Cocoa提供的一个快捷函数 NSMakeRange()
    //使用 函数 NSMakeRange()的好处是你可以在任何能够使用函数的地方使用它，
    //例如在方法调用中将其作为参数进行传递
    NSRange range3 =NSMakeRange(17, 4);
	 //   [anObject flarbulateWithRange:NSMakeRange(13, 15)];//[anObject flarbulateWithRange:(range.loc , range.length)];相当于传入两个参数
    /*
     
     struct object flarbulateWithRange:(struct)a{
     
     anObject.loc=a.loc;
     anobject.length=a.length
     return anobject;
     
     }
     */
    
    /************************  几何数据类型   CG前缀 *********************/
    /*
     
     CG Core Graphics框架提供，用来进行2D渲染  C语言写得代码
     
     */
    //CGPoint表示笛卡尔平面中的一个坐标（x,y）
    /*
     struct CGPoint
     {
        float x;
        float y;
     }
     */
    
    
    //CGSize用来存储长度和宽度
    /*
     struct CGPoint
     {
        float width;
        float height;
     }
     */
    
    
    //Cocoa提供一个矩形数据类型，它由坐标和大小复合而成
    /*
     
     struct CGRect
     {
        CGPoint origin;
        CGSize size;
     }
     */
    
    /*
     
     Cocoa也为我们提供了创建这些数据类型的快捷函数： CGPointMAke()/CGSizeMake()/CGRectMake()
     为什么这些数据类型是C语言结构体而不是对象呢？  性能
     程序（尤其是GUI程序）会用到许多临时的坐标，大小和矩形区域来完成工作。
     所有的OC对象都是动态分配的
     而动态分配会消耗大量的时间，增加系统开销
     */
	//    CGPointMake(12, 55);//注意此函数的后台程序  设计一个函数 里面申请一个 结构体 P 给 P.x P.y赋值返回P
    
   
    
    /***********************************   字符串操作   ********************************/
    
    
	/*************   创建字符串  **********/
	    //NSString的stringWithFormat方法就是这样通过 格式字符串和参数 来创建NSString
	    /*
	     类方法  + (instancetype)stringWithFormat:(NSString *)format, ... NS_FORMAT_FUNCTION(1,2);
	     OC运行时生成一个类的时候，会创建一个代表该类的 类对象
	     类对象包含指向超类、类名和类方法列表的指针，还包含一个long类型的数据，为新创建的实例对象指定大小（一字节为单位）
     
     如果你在声明方法时添加 加号 就是这个方法定义 为类方法。这个方法属于类对象（而不是类的实例对象），通常用于创建新的实例。
     我们称这种用来创建新对象的类方法为工厂方法
     
     类方法可以用来访问全局数据
     
     减号为实例方法需要实例对象才能使用
     */
	//    NSString * string =@"niaho";
	//    
	//    NSString * height;
	//    height = [NSString stringWithFormat:@"your height is %d feet, %d inches",5,11];

    
    
    //NSString 中 关于大小 好用的方法 实例方法 length它返回的是字符串中的字符的个数
    //NSString length方法能精确无误的处理各种语言的字符串  C语言的strlen()会因为字符占用的空间可能多余1个字节而出错
    
	//    NSString * height;
	//    NSUInteger length=[height length];
	//    if (length >35) {//[height length]
	//        NSLog(@"wow ,you are really tall");
	//    }
	    
    
	/**************    字符串比较  *************/
	    //isEqualToString 返回一个BOOL值（YES或NO）来表示两个字符串的内容是否相同
	    //注意区别tihing1==thing2  等号只判断指针数值，而不是它们所指的对象
	    //如果你想检测两个对象是否为同一个事物，就应该使用运算符 ==
	    //如果是想查看是否相等（即这两个字符串是否内容相同）那么就要使用isEqualToString
	//    NSString * thing1 =@"hello 5";
	//    NSString * thing2 =[NSString stringWithFormat:@"hello %d",5];
	//    if ([thing1 isEqualToString:thing2]) {
	//        NSLog(@"They are the same!");
	//    }
    
    
    //compare 接收对象和传递过来的字符串 逐个 进行比较，它返回一个NSComparisonResult（也就是一个enum枚举型）来显示结果
    /*
    enum
    {
        NSOrderedAscending=-1,
        NSOrderedSame,
        NSOrderedDescending
    };
    typedef NSInteger NSComparisonResult;
    */
	//    [@"aaardvarrk" compare:@"zygote"];
    
    
    //不区分大小写比较
    //compare 进行的是区分大小写的比较
    //(thing1) compare: (thing2) options: (NSCaseInsensitiveSearch | NSNumericSearch]==NSOrderedSame)
    //options参数是一个掩位码。你可以使用位或bitwise-OR运算符（|）来添加选项标记
    //一些常用的选项如下：NSCaseInsensitiveSearch：不区分大小写字符
    //                 NSLiteralSearch：进行完全比较，区分大小写字符
    //                 NSNumericSearch：比较字符串的字符个数，而不是字符串值
	//    if ([thing1 compare:thing2 options:NSCaseInsensitiveSearch | NSNumericSearch]==NSOrderedSame) {
	//        NSLog(@"they match!");
	//    }
	    
	    
	/************    字符串内是否还包含别的字符串   *************/
	    //两种方法：
	    //      1、检查字符串是否以另一个字符串开头
	    //      2、判断字符串是否以另一个字符串结尾
	    
	//    NSString * fileName = @"draft-chaper.pages";
	//    if ([fileName hasPrefix: @"draft"]) {
	//        NSLog(@"dra");
	//        //是否以另一个字符串开头
	//    }
	//    if ([fileName hasSuffix: @".mov"]) {
	//        NSLog(@"mov");
	//        //是否以另一个字符串结尾
	//    }
    
    //字符串内的某处是否包含其他字符串，请使用rangeofString
    //传递的是要查找的字符串，它会返回一个NSRange结构体，告诉你与这个字符串相匹配的部分在在哪里以及能够匹配上的字符个数
    //返回的range.location为6，range.length为7.如果传递的参数在接收字符串中没有找到，那么range.location则等于NSNotFound
	//    NSString * fileName = @"draft-chapter.pages";
	//    NSRange range=[fileName rangeOfString:@"chapter"];//- (NSRange)rangeOfString:(NSString *)aString;
	//    NSLog(@"%lu %lu",(unsigned long)range.location,(unsigned long)range.length);
	/***********************************  可变性  ************************************/
	//    //NSString 是不可变（immutable）的：NSString 一旦被创建，便不能改变。
	//    NSString *str1=@"nihao";
	//    NSString *str2=@"hello world";
	//    str2=str1;
	//    NSLog(@"%@",str2);
    //你可以对它执行各种各样的操作，例如用它生成新的字符串，查找字符或者将它与其他字符串进行比较，但是你不能以删除字符或者添加字符的方式改变它
    //Cocoa提供了一个 NSMutableString 子类 改变字符串
    //结果是string被赋值为“hello there human 39!”

	//    NSMutableString *string =[NSMutableString stringWithCapacity:50];//创建可变字符串
	//    //- (void)appendString:(NSString *)aString;
	//    [string appendString:@"hello there"];//appendString接受参数aString,然后将其复制到接收对象的末尾。
	//    NSLog(@"%@",string);
	//    [string appendFormat:@"human %d",39];//appendFormat：的工作方式与stringWithFormat：类似，但没有创建新的字符串，而是将格式化的字符串附加在了接收字符串的末尾  ????
	//    NSLog(@"%@",string);
    //deletecharactersInRange: 方法删除字符串中的字符
    NSMutableString * friends = [NSMutableString stringWithCapacity:50];//首先创建朋友列表
    [friends appendString:@"James Bethlynn Jack Evan"];
    NSRange jackRange = [friends rangeOfString:@"jack"];//然后找到jack名字在字符串中的范围
    //jackRange.length++;
    [friends deleteCharactersInRange:jackRange];
    //假设你列出了所有的朋友的名字，但又觉得不喜欢jack了，想要把他从列表中删除，就可以这样操作
    //这个例子中，字符范围开始与15，长度为5，现在我们就可以把jack从圣诞贺卡中踢掉
    //这个字符串就剩下“james bethlynn evan”
	//    NSMutableString * string4 = [NSMutableString stringWithFormat:@"jo%dy",2];

    return 0;
}

#NSArray NSMutableArray

int main(int argc, const char * argv[])
{

    /************************    集合大家庭  *********************/
    
    //NSArray和NSDictionary,他们的实例就是为了存储其他的对象而存在的
    
    
    /************************   NSArray   *********************/
    
    /*
    NSArray是一个Cocoa类，用来存储对象的 有序 列表。你可以在NSArray中放入 任意类型 的对象：
    可以在其中放入任何类型的对象：NSString/Car/Shape/Tire或者其他你想要存储的对象，甚至可以是其他数组或字典对象
    只要拥有一个NSArray对象，就可以通过各种方式来操作它：
                    比如让某个对象的实例变量指向这个数组
                    将该数组当作参数传递给方法或函数。
                    获取数组中所存对象的个数
                    提取某个索引所对应的对象，查找数组中的对象，遍历数组
     NSArray类有两个限制。
        一：它只能存储OC对象，而不能存储原始C语言基础数据类型，如int/float/enum/struct/NSArray中的随机指针
        二：不能在其中存储nil（对象零值或NULL值）
     
    */
    
    
    //与NSString一样，NSArray创建的是不可变对象的数组：一旦你创建了一个包含特定数量的对象的数组，他就固定下来了
    //你既不能添加任何元素也不能删除任何元素。
    //当然数组中包含的对象是可以改变的（比如Car在安全检查失败后可以获得一套新的Tire）
    //但数组对象本身是一直都不会改变的
    

    //创建一个新的NSArrray。发送一个以逗号分隔的对象列表，  在结尾添加nil代表列表结束（这就是不能在结尾中加入nil原因）
	//    NSArray * array =[NSArray arrayWithObjects:@"one",@"two" ,@"three",nil];
	//    NSArray * array2 =@[ @"one",@"two",@"three" ];
    
    //通过字面量访问数组的语法与C语言中访问数组项的语法类似
	//    NSArray * array1 =[NSArray arrayWithObjects:@"one",@"two" ,@"three",nil];
	//    NSLog(@"%@",array1);//只要有了一个数组，就可以获取它所包含的对象的个数：
	//    id  myObject =array1[1];
	//    NSLog(@"%@",myObject);
	//    NSLog(@"%@",[array1 objectAtIndex:2]);//- (id)objectAtIndex:(NSUInteger)index;也可以获得特定索引处的对象
	//    NSLog(@"%lu",(unsigned long)[array1 count]);//- (NSUInteger)count;
	//    NSArray * array1 =[NSArray arrayWithObjects:@"one",@"two" ,@"three",nil];
	//    //你可以结合计数和取值功能来输出数组中的内容
	//    for (NSInteger i=0; i<[array1 count]; i++) {
	//        NSLog(@"index %ld has %@.",(long)i,[array1 objectAtIndex:i]);
	//    }

	//    //你也可以使用数组字面量语法来写以上代码
	//    for (NSInteger i=0; i<[array1 count]; i++) {
	//        NSLog(@"index %ld has %@.",(long)i,array1[i]);
	//    }
	//    NSLog(@" %@",[array1 objectAtIndex:208000]); //注意：如果你引用的索引大于数组中对象的个数，那么Cocoa在运行时会输出错误。
	//使用 - (NSArray *)componentsSeparatedByString:(NSString *)separator 切分数组
	//    NSString * string5 =@"oop:ack:bork:greeble:ponies";
	//    NSArray * chunks =[string5 componentsSeparatedByString:@":"];
	//    NSLog(@"%@",chunks);
	    //使用 来合并NSArray中的元素并创建字符串
	//    NSString * string5 =@"oop:ack:bork:greeble:ponies";
	//    NSArray * chunks =[string5 componentsSeparatedByString:@":"];
	//    string5 =[chunks componentsJoinedByString:@":-)"];
	//    NSLog(@"%@",string5);
	    
	/**********************************   NSMutableArray  可变数组     ******************************/
    
    //弥补NSArray类的不足，可变数组类，这样就可以随意地添加或删除数组中的对象了

    //    NSMutableArray * array6 =@"nihao";//报警
    //    [array5 addObject:array6];
    //    NSLog(@"%@",array5);
    //    NSMutableArray * array7 =@[@"nahai",@"nihao",@"nini"];//报警
    //    NSLog(@"%@",array5);

    //创建 新的 可变的 数组  使用 - (void)addObject:(id)anObject;添加元素
    
    /*
     for (NSInteger i=0; i <4; i++) {
     Tire * tire = [Tire new];
     [array addobject: tire];
     }
     */
    
	//    NSMutableArray * array5 =[NSMutableArray arrayWithCapacity:17];//容量只是参考
	//    [array5 addObject:@"henhao"];
	//    NSLog(@"%@",array5);
	//    NSString * string5 =@"oop:ack:bork:greeble:ponies";
	//    NSArray * chunks =[string5 componentsSeparatedByString:@":"];
	//    [array5 addObject:chunks];
	//    NSLog(@"%@",array5);
    /*
     删除特定索引处的对象。
     - (void)removeLastObject;
     - (void)removeObjectAtIndex:(NSUInteger)index;
     - (void)replaceObjectAtIndex:(NSUInteger)index withObject:(id)anObject;
    */
    
	//    [array5 removeLastObject];
	//    NSLog(@"%@",array5);
	//    [array5 removeObjectAtIndex:0];//从0开始
	//    NSLog(@"%@",array5);
    return 0;
}

#NSDictionary NSMutableDictionary

int main(int argc, const char * argv[])
{

    /*****************    字典（dictionary关键字）   *********************/
    
    /*
     NSDictionary：就是关键字及其定义的集合
     
     NSDictionary能在给定的关键字（通常是一个NSString字符串）下存储一个数值（可以是任何类型的OC对象），然后你就可以用这个关键字来查找相应地数据。
     因此假如你有一个存储了某人所有联系方式NSDictionary，那么你可以对这个字典说“给我关键字home-address下地值”或者“给我关键字email-address下的值”。
     
     比数组好的地方：
     字典（散列表或关联数组）：使用的是键查询的优化方式。它可以立即找出要查询的数据，而不需要遍历整个数组。对于频繁的查询和大型的数据集来说，使用字典比数组快
     
     
     NSDictionary：就像NSString和NSAarray一样是不可变的对象。
     但是 NSMutableDictionary 类允许你随意添加和删除字典元素。
     
     在创建新的 NSDictionary时 就需要提供该字典所存储的全部对象和关键字
     
    */
    
    /********************        创建 不变字典        *****************/
    /*  方法一：
     NSObject *obj = [NSObject new];
     + (instancetype)dictionaryWithObjectsAndKeys:(id)firstObject, ... NS_REQUIRES_NIL_TERMINATION;
     */
	//    NSObject *p1 = [NSObject new];
	//    NSObject *p2 = [NSObject new];
	//    NSObject *p3 = [NSObject new];
	//    NSObject *p4 = [NSObject new];
	//    NSDictionary *persons = [NSDictionary dictionaryWithObjectsAndKeys:p1, @"zs", p2, @"ls", p3, @"ww", p4, @"zl", /*obj, @"obj",*/ nil];
	//    NSLog(@"persons: %@", persons);
    /*  
     方法二：字面量语法
     */
    NSObject *p1 = [NSObject new];
    NSObject *p2 = [NSObject new];
    NSObject *p3 = [NSObject new];
    NSObject *p4 = [NSObject new];
    
    NSDictionary *persons = @{@"zs":p1, @"ls":p2, @"ww":p3, @"zl":p4};//大括号
	//    NSLog(@"persons: %@", persons);
    
    /********************        根据key来获取字典中相应的对象         *****************/
    
    // 1. objectForKey
    //- (id)objectForKey:(id)aKey;
    
    //    NSString * somePerson = [persons objectForKey:@"ls"];
    //    NSLog(@"%@",somePerson);
    
    // 2. 新语法
    NSObject *obj = persons[@"ls"];
    
    NSLog(@"lisi: %@", obj);
    
    NSArray *allKeys = [persons allKeys]; //  提取出字典中所有Key放入一个新的数组中
    NSLog(@"allKeys: %@", allKeys);
    
    /********************         创建可变字典       ********************/
    
    NSMutableDictionary *persons2 = [NSMutableDictionary dictionary];
    
    //+ (instancetype)dictionaryWithCapacity:(NSUInteger)numItems;
	//    NSMutableDictionary *persons3 = [NSMutableDictionary dictionaryWithCapacity:50];//创建可变字典

    // 通过其他的字典来给字典添加元素
    [persons2 addEntriesFromDictionary:persons];
    NSLog(@"persons2:%@", persons2);
    
    /*------------------向可变字典添加对象-------------------*/
    NSObject *p5 = [NSObject new];
    [persons2 setObject:p5 forKey:@"tq"];
    
    NSLog(@"persons2: %@", persons2);
    
    NSObject *p6 = [NSObject new];
    [persons2 setObject:p6 forKey:@"tq"]; //如果对字典中已有的关键字使用setobject: forkey:方法，将会用新值替换掉原来的数值
                                            //如果对已经存在键赋值的话，会覆盖掉原来的value
    NSLog(@">>>persons2: %@", persons2);
    
    /*------------------从向可变字典移除对象-------------------*/
    [persons2 removeObjectForKey:@"tq"];
    NSLog(@"remove:%@", persons2);

    //
    
    /**********************************￥￥￥￥￥￥******************************************
     
     * 与NSArray一样，没有适用于NSMutableDictionary(可变字典)的字面量初始化方法
     * 不要创建NSString、NSArray、NSDictionary子类
     * 类簇方式实现：即它们是一群隐藏在通用接口之下的与实现相关的类
     *
     *
     *
     ****************************************************************************/
    
    return 0;
}

# 枚举

int main(int argc, const char * argv[])
{

    /*
     4种方法遍历数组：索引、使用NSEnumerator、使用快速枚举、代码块方法
     
     //4种方法来遍历数组了：
     //                  1、通过索引
     //                  2、使用NSEnumerator
     //                  3、使用快速枚举
     //                  4、最新的  代码块方法
     
    
     如果使用的不是10.5版本之前的老爷机，建议使用快速枚举或代码块，因为他们更简洁快速。顺便提一下，代码块只在APPle LLVM编译器上才会有效
     如果你还要支持MAc OS X 10.4或更早系统
     
     建议最新机子上最好使用  快速枚举 或 代码块  更简洁快速
     只有真的需要使用索引数组时才应使用-objectAtIndex方法，例如跳跃浏览数组或同时遍历多个数组时
     代替快速枚举好处是：
        代码块可以让循环操作并发执行，而通过快速枚举，执行操作要一项项的线性完成。
    */
    
    
	/*******************************  枚举     ****************************/
    //用于遍历数组
    
    /*
     NSArray经常要对数组的 每个元素 都执行 同一 操作
     你可以编写一个从0到[array count]的循环来读取每个索引处对象,
     也可以使用NSEnumerator,Cocoa可以用它来表示集合中迭代出的对象。
     遍历数组三种方式：
        （1）for循环
        （2）枚举器
        （3）快速枚举
     想要使用NSEnumerator需要通过objectEnumerator向数组请求枚举器
     如果你想从后往前浏览某个集合，还有一个reverseObjectEnumerator方法可以使用  反向枚举
     在获得枚举器之后，便可以开始一个while循环，每次循环都向这个枚举器请求它的nextObject(下一个对象)：
     nextObject返回nil值时，循环结束。
     这也是不能在数组中存储nil值的另一个原6因：我们没有办法判断nil是存储在数组中得数值还是代表循环结束标志
     对可变数组进行枚举操作时，有一点需要注意：你不能通过添加或删除对象这类方式来改变数组的容量。如果这么做了，枚举器就会出现混乱，你也会获得定义结果（undefined result）。
     “未定义结果”可以代表任何意思,可以是“唉，好像重复了”，也可能是“噢，我的程序崩溃了”等等
     */
  
	//    NSArray * array=@[@"one",@"two",@"three",@"four"];
	//    NSEnumerator * enumerator1=[array objectEnumerator];//通过objectEnumerator向数组请求枚举器// 生成一个正向的枚举器
	//    id obj1;
	//    while (obj1 = [enumerator1 nextObject]) {
	//        NSLog(@"obj1=======%@", obj1);
	//    }
	//    
	//    NSEnumerator *enumerator2 = [array reverseObjectEnumerator]; // 反向枚举器  考察的是数组的方法 不是枚举器的方法
	//    id obj2;
	//    while (obj2 = [enumerator2 nextObject]) {//枚举器只有- (id)nextObject;//- (NSArray *)allObjects;
	//        NSLog(@"obj2=======%@", obj2);
	//    }
	
	    
	//    NSMutableArray *mtArray1 = [NSMutableArray arrayWithCapacity:50]; // 创建一个可变数组
	//    [mtArray1 addObject:@"one"]; // 往可变数组添加一个新的元素
	//    NSObject *newObj1 = [NSObject new];
	//    [mtArray1 addObject:newObj1];
	//    [mtArray1 addObject:@"one1"];
	//    [mtArray1 addObject:@"one2"];
	//    [mtArray1 addObject:@"one3"];
	//    
	//    NSEnumerator *enumerator1 = [mtArray1 objectEnumerator]; // 生成一个正向的枚举器
	      //整个循环代码如下所示
	//    id obj1;
	//    while (obj1 = [enumerator1 nextObject]) {//id obj1 = [enumerator1 nextObject]书上错误
	//        NSLog(@"obj1=======%@", obj1);
	//    }

	/*************************************     快速枚举       **************************************/
    
    /*
     快速枚举不能在旧的MAc系统上运行  MAC OS X 10.5之前使用
     
     这个循环体将会遍历数组中得每一个元素，并且用变量string来存储每一个数组值。它比枚举器语法更加简洁快速
     为什么我们要使用它来代替快速枚举
     因为通过代码块可以让循环操作并发执行，而通过快速枚举，执行操作要一项项地线性完成
     */
	//    
	//    NSArray * array=@[@"one",@"two",@"three",@"four"];
	//    for (NSString * string in array) {
	//        NSLog(@"i found %@ ",string);
	//    }
	//    
    
	/*********************************      代码块方法            **********************************/
    /*
     苹果在NSString中通过代码块枚举对象的方法
     - (void)enumerateObjectsUsingBlock:(void (^)(id obj, NSUInteger idx, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
     代替快速枚举好处是：
     代码块可以让循环操作并发执行，而通过快速枚举，执行操作要一项项的线性完成。
     */
    
	//    [array enumerateObjectsUsingBlock:^(NSString * string,NSUInteger index,BOOL * stop){NSLog(@"i found %@",string);}];

    
    return 0;
}
