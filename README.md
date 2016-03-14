# runtime 学习小代码   
//大神不要见笑  有问题请指点一二

#import <Foundation/Foundation.h>
#import <objc/runtime.h>


@interface MyClass : NSObject

@end

@implementation MyClass

@end

void myMethodIMP(id self,SEL _cmd){
    NSLog(@"runtime hello");
}


int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // insert code here...
        NSLog(@"Hello, World!");
        
        NSLog(@"%s",@selector(test));
        NSLog(@"%lu",strlen(@selector(test)));
        
        char *s = calloc(100, sizeof(char));
        strcat(s,@selector(test));
        strcat(s,@selector(test));
        NSLog(@"%s",s);
        free(s);
        
        class_addMethod([MyClass class], @selector(myMethod), (IMP)myMethodIMP, "v@:");
        MyClass *myObject = [[MyClass alloc] init];
        
        [myObject performSelector:@selector(myMethod)];

        
    }
    return 0;
}


2016-03-14 15:25:44.207 KKBOX[5786:187150] Hello, World!
2016-03-14 15:25:44.208 KKBOX[5786:187150] test
2016-03-14 15:25:44.208 KKBOX[5786:187150] 4
2016-03-14 15:25:44.208 KKBOX[5786:187150] testtest
2016-03-14 15:25:44.209 KKBOX[5786:187150] runtime hello
Program ended with exit code: 0
