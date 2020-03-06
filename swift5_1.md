```
import Cocoa

enum HttpError: Error {
    case authError
    case netWorkError
    case serviceError
}

class ViewController: NSViewController {

    override func viewDidLoad() {
        super.viewDidLoad()

        // Do any additional setup after loading the view.
        
        // 常量 和 变量 声明
        // 常量 复值之后值不可变，变量可变
        let num1 = 10;
        var num2 = 5;
        let a = 1, b = 2, c = 3;
        var aa = 1, bb = 2, cc = 3;
        
        // 类型注释，与采用类型推导性能上差距很小
        // 1000000次循环相差不到一秒
        let num3: Int = 1;
        var bbb: [Int] = [1,2,3];
        var ccc: String = "str";
        
        // 控制台输出
        var ops = "";
        print(a,bbb, separator: "--", terminator: "\r\n", to: &ops);
        print(ops);
        
        // 代码注释  此为单行注释
        /*
         此为多行注释
         */
        
        // 整数边界
        let uint8_min = UInt8.min; // 0
        let uint8_max = UInt8.max; // 255
        
        let int8_min = Int8.min; // -128
        let int8_max = Int8.max; // 127
        
//         let tooBig: Int8 = Int8.max + 1; // 编译错误
        // Arithmetic operation '127 + 1' (on type 'Int8') results in an overflow
        
        // 采用类型推导声明的不同类型的变量做运算时需要类型转换
        // swift是一种类型安全的语言，编译代码时执行类型检查
        let aInt = 3; // 整型
        let aDouble = 3.94; // 浮点型
//        let aAdd = aInt + aDouble; // 编译错误
        // Binary operator '+' cannot be applied to operands of type 'Int' and 'Double'
        let aAdd = Double(aInt) + aDouble;
        print(aAdd); // 6.9399999999999995
        let aCastInt = Int(aAdd);
        print(aCastInt); // 6
        
        // 进制
        let int = 17; // 十进制数表示17
        let binary = 0b10001; // 二进制数表示17
        let octl = 0o21; // 八进制数表示17
        let hex = 0x11; // 十六进制数表示17
        
        // 别名
        typealias MyString = String;
        let myString: MyString = "我";
        print(myString);
        
        // 元祖
        // 不同的数据类型可以放在一起
        // 不适合创建复杂数据结构；反之，请用类或结构
        let tup1: (Int, String)?
        tup1 = (101, "101");
        print(tup1!.0, tup1!.1);
        
        let tup2:(code:Int, info:String)?;
        tup2 = (102, "102");
        print(tup2!.code, tup2!.info);
        
//        var aaaa:Int;
//        print(aaaa); // 编译错误
        // Variable 'aaaa' used before being initialized
        
        // 可选项（Optionals），用在变量的值可能为空时。
        // 有值（可解包获得该值） 或 nil
        
        // 非可选不能使用 nil 初始化
//        let p: String = nil; // 编译错误
        // 'nil' cannot initialize specified type 'String'
        // 'nil' cannot initialize specified type 'String' Add '?' to form the optional type 'String?'
        
        // 可选项默认值为nil
        // OC中nil指向一个不存在的对象的指针，swift中不是指针，是一个可选项的缺省值。
        let op1: Int?;
//        print(op1!) // 错误
        // Unexpectedly found nil while unwrapping an Optional value
        // Constant 'op1' used before being initialized
        
        // 强制解包 名称后加!
        // 强制解包的时候，一定要确认其包含值。
        let op2: Int? = 2;
        print(op2!);
        
        // 可选项判断
        if (op2 != nil) {
            print(op2!);
        }
        
        // 可选绑定
        // if 的可选绑定只在if中可用
        // guard 的可选绑定在其外部也可用
        let op3: Int? = 2;
        if let top = op3 {
            print(top);
        }
//        print(top); // 不可用
        guard let top = op3 else {
        }
        print(top); // 可用
        
        // 隐式解包
        let op4: Int! = nil;
        print(op4);
        
//        let yop: String! = nil;
//        let aStr: String = yop;
//        print(aStr); // 运行错误，崩溃
        // Unexpectedly found nil while implicitly unwrapping an Optional value
        
        // Error
        // 执行一个可能抛出错误的函数时，需要在其前用try，并catch
        do {
            try aExec1();
        } catch HttpError.serviceError {
            do {
                try aError2();
            } catch HttpError.authError {
              
            // 必须要有catch所有，否则编译报错
            // Errors thrown from here are not handled because the enclosing catch is not exhaustive
            } catch {
                
            }
        
        // 必须要有catch所有，否则编译报错
        // Errors thrown from here are not handled because the enclosing catch is not exhaustive
        } catch {
            
        }
        
        // 断言  条件为 false 时，代码中断执行
        let num = -1;
//        assert(num > 0, "num不能为负数");
        if (num < 0) {
//            assertionFailure("num不能为负数"); //!< 陈述条件的信息
        }
        // 前置条件，release环境下也生效
//        precondition(num > 0, "num不能为负数");
        
        
    }
    func aExec1() throws {
        do {
            try aError1();
        } catch let error as HttpError {
            throw error;
        }
    }
    func aError1() throws {
        throw HttpError.serviceError;
    }
    func aError2() throws {
        throw HttpError.authError;
    }

    override var representedObject: Any? {
        didSet {
        // Update the view, if already loaded.
        }
    }


}

```
##如果您觉得此篇文章的内容对您有所帮助，可以捐赠作者，非常感谢！！！^ _ ^
![谢谢支持.png](https://upload-images.jianshu.io/upload_images/15047809-8740fd2723d97fda.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
