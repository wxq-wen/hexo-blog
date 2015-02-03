title: block
date: 2015-02-01 16:23:49
tags: block
---


#import <Foundation/Foundation.h>


typedef double (^MKSampleMultiply2BlockRef)(double c ,double d);

typedef double (^MKSampleMultiplyBlockRef)(void);

int globalVal = 100;//全局变量



int main(int argc, const char * argv[])
{
 
    /*
    代码块可以访问与它相同的（本地）有效范围内声明的变量，也就是说代码块可以访问与它同时创建的有效变量
     */
//    
//    int value=6;
//    int (^ multiply_block)(int number) = ^ (int number){return (value * number);};// 6 * 7=42；
//    int result = multiply_block(7);
//    printf("Result= %d\n",result);
    
    // 关于参数和返回值的一些省略做法
    //        // 1.如果代码块不适用于传参数，可以将参数列表省略
    //        // 2.代码块中有return语句，那么代码块的返回值类型就是return值的类型，可省略返回值类型
    //        // 3.返回值省略时，表达式若有多个return，则所有return返回值的类型必须相同
    
    
//    
    //使用代码块时通常不需要创建一个代码块变量，而是在代码块中内联代码块中的内容。
//    NSArray *array = [NSArray arrayWithObjects:@"Amir", @"Mishal",@"Irrum",@"Adam",nil];
//    NSLog(@"array %@",array);
//    NSArray * sortedArray = [array sortedArrayUsingComparator:^(NSString *object1,NSString *object2){return [object1 compare:object2];}];
//    NSLog(@"Sorted Array %@",sortedArray);
//    
    
    //typedef 关键字  减少编写代码时出错率
    //使用typedef来定义一个相同类型的代码块类型
    /*
     
     typedef double (^MKSampleMultiply2BlockRef)(double c ,double d);
     定义了一个名称为 MKSampleMultiply2BlockRef 的代码块变量，它包含两个双浮点型参数并返回一个浮点型数值
     其他：
     typedef void (^MKSampleVoidBlockRef)(void);
     typedef void (^MKSampleStringBlockRef)(NSString *);
     typedef double (^MKSampleMultiplyBlockRef)(void);
     使用方法：
     */
//    MKSampleMultiply2BlockRef multiply2 = ^(double c ,double d){ return c*d; };
//    printf("%f ,%f",multiply2(4,5),multiply2(5,2));
//    
    /*
     代码块和变量
     
     代码块被声明后会捕捉创建点时的状态。
     代码块可以访问函数用到的标准类型的变量：
     （1）全局变量，包括在封闭范围内声明的本地静态变量
     （2）全局函数（明显不是真实的变量）
     （3）封闭范围内的参数
     （4）函数级别（即与代码块声明时相同的级别）的 _block 变量。它们是可以修改的变量。
     （5）封闭范围内的非静态变量会被获取为常量
     （6）OC实例变量
     （7）代码块内部的本地变量
     */
    
    /*
     本地变量：就是与代码块在同一范围内声明的变量
     **在它之前有效，执行完之后再次赋值后输出结果不变**
     变量与代码块拥有相同的有效范围
     原因：因为变量是本地的，代码块会在定义时复制并保存它们的状态。
     */
//    double a=10,b=20;
//    MKSampleMultiplyBlockRef multiply = ^ (void) { return a*b;};
//    NSLog(@"%f",multiply());//200.000000
//    a=20;
//    b=50;
//    //MKSampleMultiplyBlockRef multiply = ^ (void) { return a*b;};
//    NSLog(@"%f",multiply());//200.000000
   
    /*
     全局变量：变量标记为静态的（全局的）
     */
    
//    static double a=10,b=20;//全局变量
//    MKSampleMultiplyBlockRef multiply = ^ (void) { return a*b;};
//    NSLog(@"%f",multiply());//200.000000
//    a=20;
//    b=50;
//    NSLog(@"%f",multiply());//1000.000000
    
    // 全局变量，可以在代码块内部进行改变操作
//    void (^testValBlock1)() = ^{
//        globalVal++;//int globalVal = 100 全局变量
//        NSLog(@"globalVal>>>>>>>%d", globalVal);
//    };
//    testValBlock1();
    

    
    
    /*
     参数变量：
     代码块中的参数变量与函数中的参数变量具有同样地作用。
     
     typedef double (^MKSampleMultiply2BlockRef)(double c ,double d);
     MKSampleMultiply2BlockRef multiply2 = ^(double c ,double d){ return c*d; };
     NSLog(@"%f ,%f",multiply2(4,5),multiply2(5,2));
     
     */
    
    
    
    /*
     _block变量：本地变量会被代码块作为常量获取到，如果你想修改它们的值，必须将它们声明为可修改的。
     
     有些变量是无法声明为 __block类型的，它们有两个限制：
     （1）没有长度可变的数组
     （2）没有包含可变长度数组的结构体
     
     */
//    double c=3;
//    MKSampleMultiplyBlockRef multiply3 =^(double a,double b) { c=a*b; };//这就是错的
    
//    __block double c = 3;//两个" _ _  "下划线
//    MKSampleMultiply2BlockRef multiply5=^(double a,double b){return c= (a* b);};
//    NSLog(@"%f",multiply5(10,20));
    
    // 局部变量，在定义代码块的时候获取局部变量的一个快照，所以不能在代码块内部改变此变量
    __block int inVal = 50;
    void (^testValBlock)() = ^{
        inVal++;
        NSLog(@"<<<<<<<<<<<inVal>>>>>>>%d", inVal);
    };
    inVal++;
    testValBlock();

    
    
    
    
    
    /*
     代码块内部的本地变量：这些变量与函数中的本地变量具有同样的作用。
     代码块的定义, 注意：此处的逻辑不会被执行，在调用的时候才会执行
     */
//    void(^MKSampleBlockRef)(void)=^(void){
//        double a=4;
//        double c=2;
//        NSLog(@"%f",a*c);
//    };
//    MKSampleBlockRef();
    
    
    /*
     代码块   内存管理
     代码访问OC变量时必须小心
     规则：
     如果引用一个OC对象，必须要保留它
     如果通过引用 访问了一个实例变量 要保留一次self(即执行方法的对象)
     如果通过一个数值 访问了一个实例变量，变量需要保留
     
     */
  
   return 0;
}

