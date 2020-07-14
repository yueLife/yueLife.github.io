---
layout: post
title: 单例模式
date: 2017-03-05
tag: 设计模式
---

单例模式（Singleton Pattern）是设计模式中创建型模式的一种。这种模式涉及到一个单一的类，该类负责创建自己的对象，同时确保只有单个对象被创建。这个类提供了一种访问其唯一的对象的方式，可以直接访问，不需要实例化该类的对象。

注意：  
>1、单例类只能有一个实例。  
>2、单例类必须自己创建自己的唯一实例。  
>3、单例类必须给所有其他对象提供这一实例。  

关键要素：  
>1、私有静态属性 ```privite static $_instance```，用来储存生成的唯一对象。  
>2、私有构造函数 ```privite __contruct()```，防止外部 ```new```。  
>3、私有克隆函数 ```privite function __clone()```，防止对象被复制克隆。  
>4、公共静态方法 ```public static function getInstance()```，用来访问静态属性储存的对象，如果没有对象，则创建。  
>5、关键词 ```instanceof```，检查此变量是否为该类的对象、子类、或是实现接口。  

应用方向：
>1、数据库链接。  
>2、日志操作。  
>3、web 请求。  
>4、配置管理服务。  

```bash
/**
 * @purpose: 创建一个单例类
 * Class Singleton
 */
class Singleton
{
    // 定义一个私有的静态属性
    private static $_instance;

    // 私有__construct 方法
    private function __construct()
    {
        echo 'This is a Constructed method!';
    }

    // 私有 __clone 方法，防止对象被复制克隆
    private function __clone()
    {
        // E_USER_ERROR只能通过trigger_error($msg, E_USER_ERROR)手动触发。
        // E_USER_ERROR是用户自定义错误类型，可以被set_error_handler错误处理函数捕获，允许程序继续运行。
        // E_ERROR是系统错误，不能被set_error_handler错误处理函数捕获，程序会退出运行
        trigger_error('Clone is not allow!', E_USER_ERROR);
    }

    // 单例方法，用于访问实例的公共的静态方法
    public static function getInstance()
    {
        if (!(self::$_instance instanceof self)) {
            self::$_instance = new self;
        }
        return self::$_instance;
    }

    // 测试方法
    public function test(){
        echo 'Success!';
    }
}

// 用 new 实例化 private 构造函数的类会报错
// $single = new Singleton();

// clone 对象将导致一个 E_USER_ERROR
// $single_clone = clone $single;

// 用::操作符访问静态方法获取实例
$single = Singleton::getInstance();
$single->test();
```