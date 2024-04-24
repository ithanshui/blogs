将匿名类型转换为动态类型以实现灵活的数据操作
将匿名类型转换为动态对象可以在操作数据时提供更大的灵活性。匿名类型是只读的和强类型的，这在你想要修改或扩展数据时可能会有限制。
通过将匿名类型转换为动态的ExpandoObject，你可以在运行时添加、删除或修改属性。

public static dynamic ToDynamic(object anonymousObject)
{
    var dynamicObject = new ExpandoObject() as IDictionary<string, object>;
    var properties = TypeDescriptor.GetProperties(anonymousObject);

    foreach (PropertyDescriptor property in properties)
    {
        dynamicObject.Add(property.Name, property.GetValue(anonymousObject));
    }

    return dynamicObject;
}

public static void ManipulateData()
{
    var anonymousData = new { Name = "John", Age = 30 };
    dynamic dynamicData = ToDynamic(anonymousData);

    Console.WriteLine($"Name: {dynamicData.Name}, Age: {dynamicData.Age}");

    dynamicData.Age = 35;
    dynamicData.City = "New York";

    Console.WriteLine($"Name: {dynamicData.Name}, Age: {dynamicData.Age}, City: {dynamicData.City}");
}