#设计模式 
# 建造者模式
将复杂对象的构建过程与内部表示分离开,使用分步构建的方法创建复杂对象,相同的构建流程可以创建不同的对象实例

# 核心思想
拆分开构建步骤与产品本身,链式构造,分步赋值,灵活组合,舍弃复杂构造逻辑

# 解决问题
## 构造方法参数多
构建步骤都在一个地方,参数顺序易乱,可读性差

## 重载方法麻烦
可选参数多起来后,需要大量编写重载构造函数,代码臃肿,编写麻烦

## 对象创建复杂
有的字段并非我们想要填的,但是在构造函数里必须填满参数,麻烦死板

## 创建过程易变
当已经决定了部分字段,同时需要修改部分字段时,需要直接修改构造函数


# 主要结构

## 产品类(Product)
最终要创建的复杂对象,包含大量的属性,成员字段

## 具体创建者(Builder/ConcreteBuilder)
获取产品实例,装配属性,返回装配后的对象,是抽象创建者的实现

## 抽象创建者(AbstractBuilder)
不必要,但通常会有,定义了构建产品的抽象步骤

## 指挥者(Director)
不必要,是经典的创建者模式的一部分,但现在的项目里基本不用,统一编排构建流程,按固定顺序调用创建者


# CSharp代码例子
## 产品类
```csharp
using System;
Product TextProduct = new Product();
TextProduct.Id = 1;
TextProduct.Name = "Songo's Product";
TextProduct.ShowInfo();

public class Product
{
	public string Name { get; set; }
	public int Id { get; set; }
	
	public void ShowInfo()
	{
		Console.WriteLine($"Name: {Name}, Id: {Id}");
	}
}
```

## 创建者类
```csharp
using System;
Builder MyBuilder=new Builder();
Product MyProduct=MyBuilder
		.SetName("Songo's Product")
		.SetId(1)
		.Build();
MyProduct.ShowInfo();

public class Builder
{
	private Product _product = new Product();
	public Builder SetName(string name)
	{
		_product.Name=name;
		return this;
	}
	public Builder SetId(int id)
	{
		_product.Id=id;
		return this;
	}
	public Product Build()
	{
		return _product;
	}
}

public class Product
{
    public string Name { get; set; }
    public int Id { get; set; }

    public void ShowInfo()
    {
        Console.WriteLine($"Name:{Name}, Id:{Id}");
    }
}
```