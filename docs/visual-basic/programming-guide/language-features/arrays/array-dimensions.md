---
title: "Размерность массивов в Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "массивы [Visual Basic], измерения"
  - "массивы [Visual Basic], ранжировать"
  - "массивы [Visual Basic], прямоугольные"
  - "измерения, массивы"
  - "ранжирование, массивы"
  - "прямоугольные массивы"
ms.assetid: 385e911b-18c1-4e98-9924-c6d279101dd9
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Размерность массивов в Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

*Размерность* — это направление, в котором можно изменять спецификацию элементов массива.  Массив, содержащий суммы продаж на каждый день месяца, имеет одну размерность \(день месяца\).  Массив, содержащий суммы продаж по каждому отделу на каждый день месяца, имеет два измерения \(номер отдела и день месяца\).  *Рангом* массива называется число его измерений.  
  
> [!NOTE]
>  Для определения количества измерений массива можно использовать свойство <xref:System.Array.Rank%2A>.  
  
## Работа с измерениями  
 Необходимо указывать элемент массива, указав *индекс* для каждого из его измерений.  Элементы непрерывны вдоль каждого измерения, начиная с индекса 0 до наибольшего индекса для этого измерения.  
  
 На следующем рисунке показана общая структура массивов различного ранга.  Каждый элемент на иллюстрациях указывает значения индекса при обращениях к нему.  Например, можно получить доступ к первому элементу второй строки двумерного массива, указав индексы `(1, 0)`.  
  
 ![Графическая схема одномерного массива](../../../../visual-basic/programming-guide/language-features/arrays/media/arrayexdimone.png "ArrayExDimOne")  
Одномерный массив  
  
 ![Графическая схема двухмерного массива](../../../../visual-basic/programming-guide/language-features/arrays/media/arrayexdimtwo.png "ArrayExDimTwo")  
Двумерный массив  
  
 ![Графическая схема трехмерного массива](../../../../visual-basic/programming-guide/language-features/arrays/media/arrayexdimthree.png "ArrayExDimThree")  
Трехмерный массив  
  
### Одно измерение  
 Многие массивы имеют только одно измерение, например, количество людей каждого возраста.  Единственное требование при указании элемента — необходимо указывать возраст, для которого этот элемент содержит счетчик.  Поэтому такой массив использует только один индекс.  В следующем примере объявляется переменная для хранения  *одномерного массива*  счетчиков возраста для возраста от 0 до 120.  
  
```  
Dim ageCounts(120) As UInteger  
```  
  
### Два измерения  
 Некоторые массивы имеют два измерения. Например, количество офисов на каждом этаже каждого здания на территории предприятия.  Спецификация элемента требует одновременно указания номера здания и этажа. Каждый элемент содержит счетчик для этой комбинации.  Таким образом, такой массив использует два индекса.  В следующем примере объявляется переменная для хранения  *двумерного массива*  из счетчиков офисов для зданий от 0 до 40 и этажей от 0 до 5.  
  
```  
Dim officeCounts(40, 5) As Byte  
```  
  
 Двумерный массив также называют  *прямоугольным массивом*.  
  
### Три измерения  
 Некоторые массивы имеют три измерения. Например, координаты в трехмерном пространстве.  Такой массив использует три индекса, которые в этом случае представляют координаты физического пространства x, y и z.  В следующем примере объявляется переменная для хранения  *трехмерного массива*  температуры воздуха в различных точках трехмерного объема.  
  
```  
Dim airTemperatures(99, 99, 24) As Single  
```  
  
### Более трех измерений  
 Хотя массив может иметь до 32 измерений, довольно редко их бывает более трех.  
  
> [!NOTE]
>  Многомерные массивы и массивы массивов следует использовать с осторожностью, так как при увеличении размерности массива память, необходимая для его хранения, значительно увеличивается.  
  
## Использование различных измерений  
 Предположим, требуется отслеживать суммы продаж за каждый день текущего месяца.  Можно объявить одномерный массив с 31 элементом, по одному для каждого дня месяца, как показано в следующем примере.  
  
```  
Dim salesAmounts(30) As Double  
```  
  
 Теперь предположим, что требуется отслеживать те же сведения, не только для каждого дня месяца, но и для каждого месяца в году.  Можно объявить двумерный массив с 12 строками \(для месяцев\) и 31 столбцом \(для дней\), как показано в следующем примере.  
  
```  
Dim salesAmounts(11, 30) As Double  
```  
  
 Теперь предположим, что необходимо хранить сведения за более чем один год.  Если требуется отслеживать суммы продаж в течение 5 лет, можно объявить трехмерный массив с 5 слоями, 12 строками и 31 столбцом, как показано в следующем примере.  
  
```  
Dim salesAmounts(4, 11, 30) As Double  
```  
  
 Обратите внимание, что, так как каждый индекс меняется от 0 до своего максимального значения, каждое измерение массива `salesAmounts` объявляется как меньшее на единицу, чем требуемая длина этого измерения.  Обратите внимание, что размер массива возрастает с каждым новым измерением.  Три размера массивов из предыдущих примеров — это 31, 372 и 1860 элементов, соответственно.  
  
> [!NOTE]
>  Можно создать массив без использования оператора `Dim` или предложения `New`.  Например, можно вызвать метод <xref:System.Array.CreateInstance%2A> или другой компонент, который может передавать коду массив, созданный таким же способом.  Нижняя граница такого массива может отличаться от 0.  Нижнюю границу всегда можно найти с помощью метода <xref:System.Array.GetLowerBound%2A> или функции `LBound`.  
  
## См. также  
 [Массивы](../../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [Устранение неполадок, связанных с массивами](../../../../visual-basic/programming-guide/language-features/arrays/troubleshooting-arrays.md)