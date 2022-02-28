##  Java: 重载（Overload）和重写（Override）的区别。重载的方法能否根据返回类型进行区分？

### Java重载和重写区别

Java的重载和重写体现java多态性的不同表现，重写是父类与子类之间多态性的体现，重载可以看做多态的具体表现。

Java重载(overload)，一个类中定义了多个方法名称相同，但是参数列表中，参数的个数不同/参数顺序不同/参数类型不同（至少满足一个），称为方法的重载。

```
重载规则：
(1)方法名称相同
(2)参数个数不同/参数顺序不同/参数类型不同(必须至少满足一个)
(3)可以修改的(可选因此不能作为判定重载的依据)：
 · 被重载方法可以改变返回类型
 · 被重载方法可以改变访问修饰符
 · 被重载方法可以申明抛出更广泛的异常
 · 被重载方法可以在同一个类或者子类中被重载
```

Java重写(override)，子类存在方法与父类当中的方法名字相同，并且参数个数和类型一样，返回值类型与父类相同或为派生类，称为重写。

```
重写规则:
(1)父类的方法只能在子类中进行重写
(2)参数列表和被重写方法参数列表必须完全相同，包括方法名称、参数个数和类型、返回值。
(3)返回类型与被重写方法一样，或者是父类的返回值的派生类。
(3)访问权限不能比被重写方法访问权限更低。 public>protected>default>private  如果父类为public 则子类不能为protected
(4)final方法不能被重写
(5)static方法不能被重写，但是可以重新声明。但是实际上只会调用父类的静态方法，行为不具有多态性。
(6)子类父类在同一个包，子类可以重写父类除了private和final修饰的所有方法。
(7)子类父类不同包，子类只可以重写父类public和protected的非final方法。
(8)重写方法可以抛出非强制异常(RuntimeException)，无论父类方法是否抛出异常。重写的方法可以减少或者删除强制性异常的抛出，但是不能抛出更广泛的强制异常。
(9)构造方法不能重写
(10)没有继承不能重写该类方法
```

子类调用父类被重写方法，通过super关键字。

### Java重载方法能否根据返回类型进行区分

不能，因为重载方法返回值类型可以相同，其判断方法为参数列表中，参数的个数不同/参数顺序不同/参数类型不同（至少满足一个）。





ref:

https://www.runoob.com/java/java-override-overload.html