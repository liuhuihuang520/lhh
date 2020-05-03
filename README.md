1.单例模式（Singleton Pattern）
public class Singleton {
     private static final Singleton singleton = new Singleton();
//限制产生多个对象
     private Singleton(){
     }
     //通过该方法获得实例对象
     public static Singleton getSingleton(){
             return singleton;
     }  
     //类中其他方法，尽量是static
     public static void doSomething(){
     }
}

2.工厂模式
public class ConcreteCreator extends Creator {
public <T extends Product> T createProduct(Class<T> c){
             Product product=null;
             try {
                    product = (Product)Class.forName(c.getName()).newInstance();
             } catch (Exception e) {
                    //异常处理
             }
             return (T)product;         
     }
}

3.抽象工厂模式
public abstract class AbstractCreator {
     //创建A产品家族
     public abstract AbstractProductA createProductA(); 
     //创建B产品家族
     public abstract AbstractProductB createProductB();
}

4.模板方法模式
5.建造者模式
6.代理模式
7.原型模式public class PrototypeClass  implements Cloneable{
     //覆写父类Object方法
     @Override
     public PrototypeClass clone(){
             PrototypeClass prototypeClass = null;
             try {
                    prototypeClass = (PrototypeClass)super.clone();
             } catch (CloneNotSupportedException e) {
                    //异常处理
             }
             return prototypeClass;
     }
}

8.中介者模式
public abstract class Mediator {
     //定义同事类
     protected ConcreteColleague1 c1;
     protected ConcreteColleague2 c2;
     //通过getter/setter方法把同事类注入进来
     public ConcreteColleague1 getC1() {
             return c1;
     }
     public void setC1(ConcreteColleague1 c1) {
             this.c1 = c1;
     }
     public ConcreteColleague2 getC2() {
             return c2;
}
     public void setC2(ConcreteColleague2 c2) {
             this.c2 = c2;
     }
     //中介者模式的业务逻辑
     public abstract void doSomething1();
     public abstract void doSomething2();
}

9.命令模式
10.责任链模式
public abstract class Handler {
     private Handler nextHandler;
     //每个处理者都必须对请求做出处理
     public final Response handleMessage(Request request){
             Response response = null;  
             //判断是否是自己的处理级别
             if(this.getHandlerLevel().equals(request.getRequestLevel())){
                    response = this.echo(request);
             }else{  //不属于自己的处理级别
                    //判断是否有下一个处理者
                    if(this.nextHandler != null){
                            response = this.nextHandler.handleMessage(request);
                    }else{
                            //没有适当的处理者，业务自行处理
                    }
             }
             return response;
     }
     //设置下一个处理者是谁
     public void setNext(Handler _handler){
             this.nextHandler = _handler;
     }
     //每个处理者都有一个处理级别
     protected abstract Level getHandlerLevel();
     //每个处理者都必须实现处理任务
     protected abstract Response echo(Request request);
}

11.装饰模式
12.策略模式
public enum Calculator {
     //加法运算
     ADD("+"){
             public int exec(int a,int b){
                    return a+b;
             }
     },
     //减法运算
     SUB("-"){
             public int exec(int a,int b){
                    return a - b;
             }
     };
     String value = "";
     //定义成员值类型
     private Calculator(String _value){
             this.value = _value;
     }
     //获得枚举成员的值
     public String getValue(){
             return this.value;
     }
     //声明一个抽象函数
     public abstract int exec(int a,int b);
}

13.适配器模式
14.迭代器模式
15.组合模式
public class Composite extends Component {
     //构件容器
     private ArrayList<Component> componentArrayList = new ArrayList<Component>();
     //增加一个叶子构件或树枝构件
     public void add(Component component){
             this.componentArrayList.add(component);
     }
     //删除一个叶子构件或树枝构件
     public void remove(Component component){
this.componentArrayList.remove(component);
     }
     //获得分支下的所有叶子构件和树枝构件
     public ArrayList<Component> getChildren(){
             return this.componentArrayList;
     }
}

16.观察者模式
public abstract class Subject {
     //定义一个观察者数组
     private Vector<Observer> obsVector = new Vector<Observer>();
     //增加一个观察者
     public void addObserver(Observer o){
             this.obsVector.add(o);
     }
     //删除一个观察者
     public void delObserver(Observer o){
             this.obsVector.remove(o);
     }
     //通知所有观察者
     public void notifyObservers(){
             for(Observer o:this.obsVector){
                     o.update();
}
     }
}

17.门面模式
18.备忘录模式
public class BeanUtils {
     //把bean的所有属性及数值放入到Hashmap中
     public static HashMap<String,Object> backupProp(Object bean){
             HashMap<String,Object> result = new HashMap<String,Object>();
             try {
                     //获得Bean描述
                     BeanInfo beanInfo=Introspector.getBeanInfo(bean.getClass());
                     //获得属性描述
                     PropertyDescriptor[] descriptors=beanInfo.getPropertyDescriptors();
                     //遍历所有属性
                     for(PropertyDescriptor des:descriptors){
                             //属性名称
                             String fieldName = des.getName();
                             //读取属性的方法
                             Method getter = des.getReadMethod();
                             //读取属性值
                             Object fieldValue=getter.invoke(bean,new Object[]{});
                    if(!fieldName.equalsIgnoreCase("class")){
                             result.put(fieldName, fieldValue);
                    }
               }
          } catch (Exception e) {
               //异常处理
          }
          return result;
     }
     //把HashMap的值返回到bean中
     public static void restoreProp(Object bean,HashMap<String,Object> propMap){
try {
               //获得Bean描述
               BeanInfo beanInfo = Introspector.getBeanInfo(bean.getClass());
               //获得属性描述
               PropertyDescriptor[] descriptors = beanInfo.getPropertyDescriptors();
               //遍历所有属性
               for(PropertyDescriptor des:descriptors){
                    //属性名称
                    String fieldName = des.getName();
                    //如果有这个属性
                    if(propMap.containsKey(fieldName)){
                         //写属性的方法
                         Method setter = des.getWriteMethod();
                         setter.invoke(bean, new Object[]{propMap.get(fieldName)});
                    }
               }
          } catch (Exception e) {
               //异常处理
               System.out.println("shit");
               e.printStackTrace();
          }
     }
}

19.访问者模式
20.状态模式
21.解释器模式
22.享元模式
public class FlyweightFactory {
     //定义一个池容器
     private static  HashMap<String,Flyweight> pool= new HashMap<String,Flyweight>();
     //享元工厂
     public static Flyweight getFlyweight(String Extrinsic){
             //需要返回的对象
             Flyweight flyweight = null;
             //在池中没有该对象
             if(pool.containsKey(Extrinsic)){
                     flyweight = pool.get(Extrinsic);
             }else{
                     //根据外部状态创建享元对象
                     flyweight = new ConcreteFlyweight1(Extrinsic);
                     //放置到池中
                     pool.put(Extrinsic, flyweight);
             }
             return flyweight;
     }
}

23.桥梁模式

