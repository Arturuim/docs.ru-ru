---
title: "Динамическое определение фильтров предикатов во время выполнения"
description: "Динамическое определение фильтров предикатов во время выполнения."
keywords: .NET, .NET Core, C#
author: BillWagner
manager: wpickett
ms.author: wiwagn
ms.date: 12/1/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 90238470-0767-497c-916c-52d0d16845e0
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 9e724428bce09e2b2fa20b9391ad131424e16413
ms.contentlocale: ru-ru
ms.lasthandoff: 07/28/2017

---
# <a name="dynamically-specify-predicate-filters-at-runtime"></a>Динамическое определение фильтров предикатов во время выполнения

В некоторых случаях количество предикатов, которые нужно применить к исходным элементам в предложении `where`, неизвестно вплоть до времени выполнения. Одним из способов динамического определения сразу нескольких фильтров предикатов служит метод <xref:System.Linq.Enumerable.Contains%2A>, как показано в следующем примере. Пример конструируется двумя способами. Во-первых, проект запускается в результате применения фильтра к предоставленным в программе значениям. Затем проект запускается снова, когда применяются данные, введенные в среде выполнения.  
  
## <a name="to-filter-by-using-the-contains-method"></a>Фильтрование с помощью метода Contains  
  
1.  Откройте новое консольное приложение и присвойте ему имя `PredicateFilters`.  
  
2.  Скопируйте класс `StudentClass` из окна [Запрос коллекции объектов](query-a-collection-of-objects.md) и вставьте его в пространство имен `PredicateFilters` под классом `Program`. `StudentClass` предоставляет список объектов `Student`.  
  
3.  Закомментируйте метод `Main` в `StudentClass`.  
  
4.  Замените класс `Program` на следующий код.  
  
     [!code-cs[csProgGuideLINQ#26](../../../samples/snippets/csharp/concepts/linq/how-to-dynamically-specify-predicate-filters-at-runtime_1.cs)]  
  
5.  Добавьте в метод `Main` в классе `DynamicPredicates` следующую строку под объявлением `ids`.  
  
     ```csharp
     QueryById(ids);
     ```

6.  Запустите проект.  
  
7.  В консольном окне отобразятся следующие выходные данные:  
  
     Гарсия: 114  
  
     О'Доннелл: 112  
  
     Омельченко: 111  
  
8.  Следующим шагом станет повторный запуск проекта, на этот раз с данными, введенными в среде выполнения, а не с массивом `ids`. В методе `Main` измените `QueryByID(ids)` на `QueryByID(args)`.  
  
9. Запустите проект с аргументами командной строки `122 117 120 115`. Когда проект будет запущен, эти значения станут элементами `args`, параметра метода `Main`.  
  
10. В консольном окне отобразятся следующие выходные данные:  
  
     Адамс: 120  
  
     Фенг: 117  
  
     Гарсия: 115  
  
     Такер: 122  
  
## <a name="to-filter-by-using-a-switch-statement"></a>Фильтрование с помощью оператора switch  
  
1.  Оператор `switch` позволяет выбрать один из предустановленных альтернативных запросов. В следующем примере `studentQuery` использует другое предложение `where`, в зависимости от того, какой уровень оценок или год указан в среде выполнения.  
  
2.  Скопируйте следующий метод и вставьте его в класс `DynamicPredicates`.  
  
     [!code-cs[csProgGuideLINQ#27](../../../samples/snippets/csharp/concepts/linq//how-to-dynamically-specify-predicate-filters-at-runtime_2.cs)]  
  
3.  В методе `Main` замените вызов `QueryByID` на следующий вызов, который отправляет первый элемент из массива `args` как аргумент: `QueryByYear(args[0])`.  
  
4.  Запустите проект с помощью аргумента командной строки, выраженного целочисленным значением от 1 до 4.  
  
 
## <a name="see-also"></a>См. также  
 [Выражения запросов LINQ](index.md)   
 [предложение where](../language-reference/keywords/where-clause.md)

