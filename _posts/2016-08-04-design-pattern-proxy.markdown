# 普通的代理模式

在看动态代理之前，我们先看下什么是代理模式。使用代理模式，我们创建一个代理类，实现和被代理类相同接口，利用多态提供给调用方代理对象，通常代理类需要持有个被代理对象。

### Sample
场景：我们有**客户类**`Customer`,**老板类**`Boss`,**店员类**`Clerk`,

```java
/**
 * @author yanliang
 */
public class Customer {
    public void buyMerchandise(){
        
    }
}
```