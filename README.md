# php-abstract-class
php-接口抽象类的声明方式 及 多态


接口技术
 
    接口中一种特殊的抽象类， 抽象类又是一种特殊的类


    接口和抽象类是一样的作用

    因为在PHP是单继承的， 如果使用抽象类，子类实现完抽象类就不能再去继承其它的类了。

    如果即想实现一些规范， 又想继承一个其他类。就要使用接口
    
    
 
   接口和抽象类的对比
 
     1. 作用相同，都不能创建对象， 都需要子类去实现
     
     2. 接口的声明和抽象类不一样
     
     3. 接口被实现的方式不一样
 
     4. 接口中的所有方法必须是抽象方法，只能声明抽象方法（不用使用abstract修饰）
     
     5. 接口中的成员属性，只能声明常量，不能声明变量
 
     6. 接口中的成员访问权限 都必须是public, 抽象类中最低的权限protected
  
     7. 使用一个类去实现接口， 不是使用extends关键字， 而是使用implements这个词
 
          如果子类是重写父接口中抽象方法，则使用implements, 类--接口， 抽象类---接口 implements 接口---接口 extends

         可以使用抽象类去实现接口中的部分方法
         如果想让子类可以创建对象，则必须实现接口中的全部抽象方法

         可以定义一个接品口去继承另一个接品口

         一个类可以去实现多个接口（按多个规范去开发子类）, 使用逗号分隔多个接口名称

         一个类可以在继承一类的同时，去实现一个或多个接口(先继承，再实现)

     使用implements的两个目的
          1. 可以实现多个接口 ，而extends词只能继承一个父类
          2. 没有使用extends词，可以去继承一个类， 所以两个可以同时使用
     
              类的声明方式：
               class 类名{

               }

                抽象类的声明方式；
               abstract class 类名 {

               }

              接口的声明方式：
              interface 接口名{

              }


接口里面只能使用常量   不能使用变量   
 
           如下例子

                    interface Demo {
                      const HOST="localhost";
                      const USER="Admin";
                    }

                    echo Demo::HOST;     输出  localhost



接口例子
 
 
                          interface Demo{
                            const NAME="蔺雨轩";

                            function fun1();
                            function fun2();
                          }

                          interface Demo2 extends Demo{
                            function fun1();
                            function fun2();
                            function fun3();
                          }

                          interface Demo3{
                            function fun4();
                          }
                          class 	Texts1{
                            function class_s(){
                              echo "我是类";
                            }
                          }

                        class Texts2 extends Texts1 implements Demo2,Demo3{
                          function fun1(){
                            echo "fun1<br>";	
                          }
                          function fun2(){
                            echo "fun2<br>";
                          }
                          function fun3(){
                            echo "fun3<br>";
                          }
                          function fun4(){
                            echo "fun4<br>";
                          }
                          function class_s(){
                            echo "我是class_s";
                          }

                        } 


                          $p=new Texts2;
                          $p->fun1();    输出  fun1
                          $p->fun2();    输出  fun2
                          $p->fun3();    输出  fun3
                          $p->fun4();    输出  fun4
                          $p->class_s();  输出  我是class_s




   多态：  多态是面向对象的三大特性之一

        “多态”是面向对象设计的重要特性，它展现了动态绑
        定（dynamic binding）的功能，也称为“同名异
        式”（Polymorphism）。多态的功能可让软件在开发和维护
        时，达到充分的延伸性（extension）。事实上，多态最直接
        的定义就是让具有继承关系的不同类对象，可以对相同名称
        的成员函数调用，产生不同的反应效果。
 
     
 
 实现多态 例子
 
  
              
                                        interface  USB {
                                            function mount();
                                            function work();
                                            function unmount();
                                          }


                                          class Upan implements USB {
                                            function mount(){
                                              echo "U 盘挂载成功， 可以使用<br>";
                                            }

                                            function work(){
                                              echo "U 盘开始工作<br>";
                                            }

                                            function unmount(){
                                              echo "U 盘卸载成功<br>";
                                            }
                                          }

                                          class FengShan implements USB {
                                            function mount(){
                                              echo "风扇 挂载成功， 可以使用<br>";
                                            }

                                            function work(){
                                              echo "小风扇开始吹小风<br>";
                                            }

                                            function unmount(){
                                              echo "风扇卸载成功<br>";
                                            }
                                          }



                                          class DianNao {
                                            function  useUSB($usb){  //多态的用法
                                              $usb->mount();
                                              $usb->work();
                                              $usb->unmount();
                                            }
                                          }

                                          class Worker {
                                            function install(){
                                            
                                              //找到电脑
                                              $dn=new DianNao;
                                              
                                              //拿过来一些USB设备
                                              $up=new Upan;
                                              $fs=new FengShan;

                                              //向电脑是插入USB设备
                                              $dn->useUSB($fs);
                                              $dn->useUSB($up);

                                            }
                                          }


                                              $ren=new Worker;

                                              $ren->install();

 
 
 
 
 
 
 
 


