---
title: "Лямбда-выражения (Руководство по программированию в C#)"
ms.date: 2017-03-03
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- lambda expressions [C#]
- outer variables [C#]
- statement lambda [C#]
- expression lambda [C#]
- expressions [C#], lambda
ms.assetid: 57e3ba27-9a82-4067-aca7-5ca446b7bf93
caps.latest.revision: 64
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c952c72d9108775fbd0f824f82cacdab5ba91d09
ms.contentlocale: ru-ru
ms.lasthandoff: 07/28/2017

---
# <a name="lambda-expressions-c-programming-guide"></a>Лямбда-выражения (Руководство по программированию в C#)
Лямбда-выражение — это [анонимная функция](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md) , с помощью которой можно создавать типы [делегатов](../../../csharp/programming-guide/delegates/using-delegates.md) или [деревьев выражений](http://msdn.microsoft.com/library/fb1d3ed8-d5b0-4211-a71f-dd271529294b) . С помощью лямбда-выражений можно писать локальные функции, которые можно передавать в качестве аргументов или возвращать в качестве значений из вызовов функций. Лямбда-выражения особенно полезны при написании выражений запросов LINQ.  
  
 Чтобы создать лямбда-выражение, необходимо указать входные параметры (если они есть) с левой стороны лямбда-оператора [=>](../../../csharp/language-reference/operators/lambda-operator.md), и поместить блок выражений или операторов с другой стороны. Например, лямбда-выражение `x => x * x` задает параметр с именем `x` и возвращает значение `x` . Можно назначить это выражение типу делегата, как показано в следующем примере:  
  
```csharp  
delegate int del(int i);  
static void Main(string[] args)  
{  
    del myDelegate = x => x * x;  
    int j = myDelegate(5); //j = 25  
}  
```  
  
 Создание типа дерева выражений:  
  
```csharp  
using System.Linq.Expressions;  
  
namespace ConsoleApplication1  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            Expression<del> myET = x => x * x;  
        }  
    }  
}  
```  
  
 Оператор `=>` имеет такой же приоритет, как и присваивание (`=`), и является [правоассоциативным](../../../csharp/programming-guide/statements-expressions-operators/operators.md) (см. раздел "Ассоциативность" статьи об операторах).  
  
 Лямбда-операторы используются в запросах [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] на основе методов в качестве аргументов стандартных методов операторов запроса, таких как <xref:System.Linq.Enumerable.Where%2A>.  
  
 При использовании синтаксиса на основе методов для вызова метода <xref:System.Linq.Enumerable.Where%2A> в классе <xref:System.Linq.Enumerable> (как это делается в [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] на объекты и [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]) параметром является тип делегата <xref:System.Func%602?displayProperty=fullName>. Лямбда-выражение — это наиболее удобный способ создания делегата. При вызове того же метода, к примеру, в классе <xref:System.Linq.Queryable?displayProperty=fullName> (как это делается в [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)]) типом параметра будет <xref:System.Linq.Expressions.Expression?displayProperty=fullName><Func\>, где Func — это любые делегаты Func с числом входных параметров не более шестнадцати. Опять же, лямбда-выражения представляют собой самый быстрый способ построения дерева выражений. Лямбда-выражения позволяют вызовам `Where` выглядеть одинаково, хотя на самом деле объект, созданный из лямбда-выражения, имеет другой тип.  
  
 Обратите внимание: в приведенном выше примере сигнатура делегата имеет один неявный входной параметр типа `int`и возвращает значение типа `int`. Лямбда-выражение можно преобразовать в делегат соответствующего типа, поскольку он также имеет один входной параметр (`x`) и возвращает значение, которое компилятор может неявно преобразовать в тип `int`. (Вывод типов более подробно рассматривается в следующих разделах.) Делегат, вызываемый посредством входного параметра 5, возвращает результат 25.  
  
 Лямбда-выражения нельзя использовать с левой стороны оператора [is](../../../csharp/language-reference/keywords/is.md) или [as](../../../csharp/language-reference/keywords/as.md).  
  
 Все ограничения, применяемые к анонимным методам, применяются также к лямбда-выражениям. Дополнительные сведения см. в разделе [Анонимные методы](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md).  
  
## <a name="expression-lambdas"></a>Выражения-лямбды  
 Лямбда-выражение с выражением с правой стороны оператора => называется *выражением-лямбдой*. Выражения-лямбды широко используются при конструировании [деревьев выражений](http://msdn.microsoft.com/library/fb1d3ed8-d5b0-4211-a71f-dd271529294b). Выражения-лямбды возвращают результат выражения и принимают следующую основную форму.  
  
```csharp
(input-parameters) => expression
```

 Если лямбда-выражение имеет только один входной параметр, скобки можно не ставить; во всех остальных случаях они обязательны. Два и более входных параметра разделяются запятыми и заключаются в скобки:  
  
```csharp
(x, y) => x == y
```

 Иногда компилятору бывает трудно или даже невозможно определить входные типы. В этом случае типы можно указать в явном виде, как показано в следующем примере.  
  
```csharp
(int x, string s) => s.Length > x
```

 Нулевое количество входных параметры задается пустыми скобками:  
  
```csharp
() => SomeMethod()
```

 Обратите внимание, что тело выражения-лямбды может состоять из вызова метода, как было показано в предыдущем примере. Однако при создании деревьев выражений, которые вычисляются вне .NET Framework, например в SQL Server, не следует использовать вызовы методов в лямбда-выражениях. Эти методы не имеют смысла вне контекста среды CLR .NET.  
  
## <a name="statement-lambdas"></a>Лямбды операторов  
 Лямбда оператора напоминает выражение-лямбду, за исключением того, что оператор (или операторы) заключается в фигурные скобки:  
  
(входные-параметры) => { оператор; }

 Тело лямбды оператора может состоять из любого количества операторов; однако на практике обычно используется не более двух-трех.  
  
[!code-csharp[StatementLamba#1](../../../../samples\snippets\csharp\programming-guide\lambda-expressions/statements.cs#1)]

[!code-csharp[StatementLamba#2](../../../../samples\snippets\csharp\programming-guide\lambda-expressions/statements.cs#2)]

 Лямбды операторов, как и анонимные методы, не могут использоваться для создания деревьев выражений.  
  
## <a name="async-lambdas"></a>Асинхронные лямбда-выражения  
 С помощью ключевых слов [async](../../../csharp/language-reference/keywords/async.md) и [await](../../../csharp/language-reference/keywords/await.md) можно легко создавать лямбда-выражения и операторы, включающие асинхронную обработку. Например, в следующем примере Windows Forms содержится обработчик событий, который вызывает асинхронный метод `ExampleMethodAsync`и ожидает его.  
  
```csharp
public partial class Form1 : Form  
{  
    public Form1()  
    {  
        InitializeComponent();  
    }  
  
    private async void button1_Click(object sender, EventArgs e)  
    {  
        // ExampleMethodAsync returns a Task.  
        await ExampleMethodAsync();  
        textBox1.Text += "\r\nControl returned to Click event handler.\n";  
    }  
  
    async Task ExampleMethodAsync()  
    {  
        // The following line simulates a task-returning asynchronous process.  
        await Task.Delay(1000);  
    }  
}  
```

 Такой же обработчик событий можно добавить с помощью асинхронного лямбда-выражения. Чтобы добавить этот обработчик, поставьте модификатор `async` перед списком параметров лямбда-выражения, как показано в следующем примере.  
  
```csharp  
public partial class Form1 : Form  
{  
    public Form1()  
    {  
        InitializeComponent();  
        button1.Click += async (sender, e) =>  
        {  
            // ExampleMethodAsync returns a Task.  
            await ExampleMethodAsync();  
            textBox1.Text += "\nControl returned to Click event handler.\n";  
        };  
    }  
  
    async Task ExampleMethodAsync()  
    {  
        // The following line simulates a task-returning asynchronous process.  
        await Task.Delay(1000);  
    }  
}  
```  

 Дополнительные сведения о создании и использовании асинхронных методов см. в разделе [Асинхронное программирование с использованием ключевых слов Async и Await](../../../csharp/programming-guide/concepts/async/index.md).  
  
## <a name="lambdas-with-the-standard-query-operators"></a>Лямбды со стандартными операторами запросов  
 Многие стандартные операторы запросов имеют входной параметр, тип которого принадлежит к семейству <xref:System.Func%602> универсальных делегатов. Эти делегаты используют параметры типа для определения количества и типов входных параметров, а также тип возвращаемого значения делегата. Делегаты`Func` очень полезны для инкапсуляции пользовательских выражений, которые применяются к каждому элементу в наборе исходных данных. В качестве примера рассмотрим следующий тип делегата.  
  
```csharp  
public delegate TResult Func<TArg0, TResult>(TArg0 arg0)  
```  
  
 Экземпляр этого делегата можно создать как `Func<int,bool> myFunc` , где `int` — входной параметр, а `bool` — возвращаемое значение. Возвращаемое значение всегда указывается в последнем параметре типа. `Func<int, string, bool>` определяет делегат с двумя входными параметрами, `int` и `string`, и типом возвращаемого значения `bool`. Следующий делегат `Func` при вызове возвращает значение true или false, которое показывает, равен ли входной параметр 5.  
  
```csharp  
Func<int, bool> myFunc = x => x == 5;  
bool result = myFunc(4); // returns false of course  
```  
  
 Также лямбда-выражения можно использовать, когда аргумент имеет тип `Expression<Func>`, например в стандартных операторах запросов, как указано в System.Linq.Queryable. При определении аргумента `Expression<Func>` лямбда компилируется в дерево выражений.  
  
 Ниже показан метод <xref:System.Linq.Enumerable.Count%2A> , являющийся стандартным оператором запроса.  
  
```csharp  
int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };  
int oddNumbers = numbers.Count(n => n % 2 == 1);  
```  
  
 Компилятор может вывести тип входного параметра ввода; но его также можно определить явным образом. Данное лямбда-выражение подсчитывает указанные целые значения (`n`), которые при делении на два дают остаток 1.  
  
 Следующая строка кода создает последовательность, которая содержит все элементы массива `numbers` , расположенные слева от 9, поскольку это первое число последовательности, не удовлетворяющее условию:  
  
```csharp  
var firstNumbersLessThan6 = numbers.TakeWhile(n => n < 9);  
```  
  
 В этом примере показано, как определить несколько входных параметров путем их заключения в скобки. Этот метод возвращает все элементы в массиве чисел до того числа, величина которого меньше номера его позиции. Не следует путать лямбда-оператор (`=>`) с оператором "больше или равно" (`>=`).  
  
```csharp  
var firstSmallNumbers = numbers.TakeWhile((n, index) => n >= index);  
```  
  
## <a name="type-inference-in-lambdas"></a>Вывод типа в лямбда-выражениях  
 При написании лямбда-выражений обычно не требуется указывать тип входных параметров, поскольку компилятор может выводить этот тип на основе тела лямбда-выражения, типа делегата параметра и других факторов, как описано в спецификации языка C#. Для большинства стандартных операторов запросов первой входное значение имеет тип элементов в исходной последовательности. Поэтому при запросе `IEnumerable<Customer>`входная переменная считается объектом `Customer` , а это означает, что у вас есть доступ к его методам и свойствам.  
  
```csharp  
customers.Where(c => c.City == "London");  
```  
  
 Общие правила для лямбда-выражений формулируются следующим образом:  
  
-   лямбда-выражение должно содержать то же число параметров, что и тип делегата;  
  
-   каждый входной параметр в лямбда-выражении должен быть неявно преобразуемым в соответствующий параметр делегата;  
  
-   возвращаемое значение лямбда-выражения (если таковое имеется) должно быть неявно преобразуемым в возвращаемый тип делегата.  
  
 Обратите внимание: лямбда-выражения сами по себе не имеют типа, поскольку в системе общих типов изначально отсутствует понятие "лямбда-выражения". Однако иногда бывает удобно оперировать понятием "типа" применительно к лямбда-выражениям. При этом под типом понимается тип делегата или тип <xref:System.Linq.Expressions.Expression> , в который преобразуется лямбда-выражение.  
  
## <a name="variable-scope-in-lambda-expressions"></a>Область действия переменной в лямбда-выражениях  
 Лямбда-выражения могут ссылаться на *внешние переменные* (см. раздел [Анонимные методы](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)), находящиеся в области метода, в котором определена лямбда-функция, или в области типа, который содержит лямбда-выражение. Переменные, полученные таким способом, сохраняются для использования в лямбда-выражениях, даже если бы в ином случае они оказались за границами области действия и уничтожились сборщиком мусора. Внешняя переменная должна быть определенным образом присвоена, прежде чем она сможет использоваться в лямбда-выражениях. В следующем примере демонстрируются эти правила.  
  
```csharp  
delegate bool D();  
delegate bool D2(int i);  
  
class Test  
{  
    D del;  
    D2 del2;  
    public void TestMethod(int input)  
    {  
        int j = 0;  
        // Initialize the delegates with lambda expressions.  
        // Note access to 2 outer variables.  
        // del will be invoked within this method.  
        del = () => { j = 10;  return j > input; };  
  
        // del2 will be invoked after TestMethod goes out of scope.  
        del2 = (x) => {return x == j; };  
  
        // Demonstrate value of j:  
        // Output: j = 0   
        // The delegate has not been invoked yet.  
        Console.WriteLine("j = {0}", j);        // Invoke the delegate.  
        bool boolResult = del();  
  
        // Output: j = 10 b = True  
        Console.WriteLine("j = {0}. b = {1}", j, boolResult);  
    }  
  
    static void Main()  
    {  
        Test test = new Test();  
        test.TestMethod(5);  
  
        // Prove that del2 still has a copy of  
        // local variable j from TestMethod.  
        bool result = test.del2(10);  
  
        // Output: True  
        Console.WriteLine(result);  
  
        Console.ReadKey();  
    }  
}  
```  
  
 Следующие правила применимы к области действия переменной в лямбда-выражениях.  
  
-   Захваченная переменная не будет уничтожена сборщиком мусора до тех пор, пока делегат, который на нее ссылается, не перейдет в статус подлежащего уничтожению при сборке мусора.  
  
-   Переменные, вводимые в лямбда-выражении, невидимы во внешнем методе.  
  
-   Лямбда-выражение не может непосредственно захватывать параметры `ref` или `out` из метода, в котором они находятся.  
  
-   Оператор return в лямбда-выражении не вызывает возвращение значения внешним методом.  
  
-   Лямбда-выражение не может содержать оператора `goto` , оператора `break` или оператора `continue` внутри лямбда-функции, если целевой объект перехода находится вне блока. Если целевой объект находится внутри блока, то наличие оператора перехода за пределами лямбда-функции также будет ошибкой.  
  
## <a name="c-language-specification"></a>Спецификация языка C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="featured-book-chapter"></a>Важная глава книги  
 [Делегаты, события и лямбда-выражения](http://go.microsoft.com/fwlink/?LinkId=195395) в [справочном руководстве по C# 3.0, третье издание: более 250 решений для программистов на C# 3.0](http://go.microsoft.com/fwlink/?LinkId=195369)  
  
## <a name="see-also"></a>См. также  
 [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)   
 [Встроенный язык запросов LINQ](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)   
 [Анонимные методы](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)   
 [is](../../../csharp/language-reference/keywords/is.md)   
 [Expression Trees](http://msdn.microsoft.com/library/fb1d3ed8-d5b0-4211-a71f-dd271529294b)   
 [Примеры C# в Visual Studio 2008 (см. файлы примеров запросов LINQ и программу XQuery)](http://code.msdn.microsoft.com/Visual-Studio-2008-C-d295cdba)   
 [Рекурсивные лямбда-выражения](http://go.microsoft.com/fwlink/?LinkId=112395)

