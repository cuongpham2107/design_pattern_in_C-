# design_pattern_in_C-
Trong C#, có nhiều design pattern phổ biến được sử dụng để giải quyết các vấn đề khác nhau trong phát triển phần mềm. Dưới đây là một số design pattern phổ biến nhất:

<h1>1. Creational Patterns</h1>
<h3>Singleton</h3>
Mô tả: Đảm bảo rằng một lớp chỉ có một instance duy nhất và cung cấp một điểm truy cập toàn cục tới nó.
Ví dụ: Quản lý kết nối tới cơ sở dữ liệu.
```C#
public class Singleton
{
    private static Singleton _instance;
    private static readonly object _lock = new object();

    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            lock (_lock)
            {
                if (_instance == null)
                {
                    _instance = new Singleton();
                }
                return _instance;
            }
        }
    }
}
```
Factory Method
Mô tả: Định nghĩa một interface để tạo một đối tượng, nhưng để các lớp con quyết định lớp nào sẽ được khởi tạo. Factory Method cho phép một lớp hoãn việc khởi tạo đối tượng cho các lớp con.
Ví dụ: Tạo các đối tượng hình học khác nhau như hình tròn, hình vuông.
```C#
public abstract class Creator
{
    public abstract IProduct FactoryMethod();
}

public class ConcreteCreatorA : Creator
{
    public override IProduct FactoryMethod()
    {
        return new ProductA();
    }
}

public interface IProduct { }
public class ProductA : IProduct { }
```
2. Structural Patterns
Adapter
Mô tả: Chuyển đổi interface của một lớp thành một interface khác mà client mong đợi. Adapter cho phép các lớp làm việc cùng nhau mà lẽ ra không thể do không tương thích về interface.
Ví dụ: Kết nối một hệ thống cũ với một hệ thống mới.
```C#
public interface ITarget
{
    void Request();
}

public class Adaptee
{
    public void SpecificRequest() { }
}

public class Adapter : ITarget
{
    private readonly Adaptee _adaptee;

    public Adapter(Adaptee adaptee)
    {
        _adaptee = adaptee;
    }

    public void Request()
    {
        _adaptee.SpecificRequest();
    }
}
```
Decorator
Mô tả: Gắn trách nhiệm bổ sung cho một đối tượng một cách linh hoạt. Decorator cung cấp một giải pháp thay thế cho việc kế thừa để mở rộng chức năng.
Ví dụ: Thêm các chức năng bổ sung cho các component UI.
```C#
public interface IComponent
{
    string Operation();
}

public class ConcreteComponent : IComponent
{
    public string Operation()
    {
        return "ConcreteComponent";
    }
}

public class Decorator : IComponent
{
    protected IComponent _component;

    public Decorator(IComponent component)
    {
        _component = component;
    }

    public virtual string Operation()
    {
        return _component.Operation();
    }
}

public class ConcreteDecoratorA : Decorator
{
    public ConcreteDecoratorA(IComponent component) : base(component) { }

    public override string Operation()
    {
        return $"ConcreteDecoratorA({base.Operation()})";
    }
}
```
3. Behavioral Patterns
Observer
Mô tả: Định nghĩa một phụ thuộc một-nhiều giữa các đối tượng sao cho khi một đối tượng thay đổi trạng thái, tất cả các đối tượng phụ thuộc của nó đều được thông báo và cập nhật tự động.
Ví dụ: Hệ thống sự kiện, giao diện người dùng.

```C#
public interface IObserver
{
    void Update(ISubject subject);
}

public interface ISubject
{
    void Attach(IObserver observer);
    void Detach(IObserver observer);
    void Notify();
}

public class ConcreteSubject : ISubject
{
    private List<IObserver> _observers = new List<IObserver>();

    public void Attach(IObserver observer)
    {
        _observers.Add(observer);
    }

    public void Detach(IObserver observer)
    {
        _observers.Remove(observer);
    }

    public void Notify()
    {
        foreach (var observer in _observers)
        {
            observer.Update(this);
        }
    }
}

```
Strategy
Mô tả: Định nghĩa một họ thuật toán, đóng gói từng thuật toán, và làm cho chúng có thể hoán đổi cho nhau. Strategy cho phép thuật toán thay đổi độc lập với các client sử dụng nó.
Ví dụ: Các thuật toán sắp xếp khác nhau.

```C#
public interface IStrategy
{
    void Execute();
}

public class ConcreteStrategyA : IStrategy
{
    public void Execute()
    {
        // Implement algorithm A
    }
}

public class Context
{
    private IStrategy _strategy;

    public Context(IStrategy strategy)
    {
        _strategy = strategy;
    }

    public void SetStrategy(IStrategy strategy)
    {
        _strategy = strategy;
    }

    public void ExecuteStrategy()
    {
        _strategy.Execute();
    }
}
```
Sử dụng các design pattern này trong C# có thể giúp bạn xây dựng các ứng dụng linh hoạt, dễ bảo trì và có thể mở rộng.
