先讲反射机制，反射就是程序运行期间JVM会对任意一个类洞悉它的属性和方法，对任意一个对象都能够访问它的属性和方法。依靠此机制，可以动态的创建一个类的对象和调用对象的方法。

其次就是反射相关的API，只讲一些常用的，比如获取一个Class对象。Class.forName(完整类名)。通过Class对象获取类的构造方法，class.getConstructor。根据class对象获取类的方法，getMethod和getMethods。使用class对象创建一个对象，class.newInstance等。

最后可以说一下反射的优点和缺点，优点就是增加灵活性，可以在运行时动态获取对象实例。缺点是反射的效率很低，而且会破坏封装，通过反射可以访问类的私有方法，不安全。

如果了解JVM可以结合JVM的相关知识说。

> 这里具体结合什么说？