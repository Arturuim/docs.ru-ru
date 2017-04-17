---
title: "Transfer | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dfcfa36c-d3bb-44b4-aa15-1c922c6f73e6
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Transfer
В этом разделе описывается перенаправление в модели трассировки действий [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].  
  
## Определение перенаправления  
 Перенаправления между действиями передают причинно\-следственную связь между событиями в связанных действиях внутри конечных точек.  Два действия связываются перенаправлениями при потоке управления от одного из этих действий к другому, например когда вызов метода пересекает границы действия.  В [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] при получении службой данных действие Listen At перенаправляется на действие Receive Bytes, где создается объект сообщения.  Перечень сценариев сквозной трассировки с соответствующими схемами действий и трассировки см. в разделе [Сценарии сквозной трассировки](../../../../../docs/framework/wcf/diagnostics/tracing/end-to-end-tracing-scenarios.md).  
  
 Для выдачи трассировки перенаправлений задайте параметр `ActivityTracing` в источнике трассировки, как показано в предыдущем примере кода.  
  
```  
<source name="System.ServiceModel" switchValue="Verbose,ActivityTracing">  
```  
  
## Использование перенаправления для корреляции действий внутри конечных точек  
 Действия и перенаправления позволяют пользователю с определенной вероятностью найти первопричину ошибки.  Например, если при перенаправлении от действия M на действие N и обратно \(в компонентах M и N соответственно\) сразу же после перенаправления обратно на M происходит сбой, можно сделать вывод, что это скорее всего связано с передачей действием N данных обратно действию M.  
  
 Трассировка перенаправления выдается от действия M к действию N при передаче управления от M к N.  Например, N выполняет некоторую работу для M в связи с тем, что вызов метода пересекает границы действий.  Действие N может уже существовать или быть создано.  Действие N порождается действием M, когда N представляет собой новое действие, выполняющее некоторую обработку для M.  
  
 За перенаправлением от M к N не обязательно следует перенаправление обратно от N к M.  Это связано с тем, что M может создать некоторую работу в N и не следит за тем, когда N завершит эту работу.  Фактически действие M может быть прекращено до того, как N завершит свою задачу.  Это происходит в действии Open ServiceHost \(M\), которое порождает действия прослушивателя \(N\) и затем прекращается.  Перенаправление обратно от N на M означает, что действие N завершило обработку, относящуюся к действию M.  
  
 Действие N может продолжать выполнять другую обработку, не относящуюся к действию M, например существующее действие структуры проверки подлинности \(N\) продолжит получать запросы на вход \(M\) от других действий входа.  
  
 Между действиями M и N может и не быть отношения вложенности.  Это может произойти по двум причинам.  Первая \- когда действие M не осуществляет наблюдение за обработкой, выполняемой действием N, даже если действие M инициировало действие N.  Вторая \- когда N уже существует.  
  
## Пример перенаправления  
 Ниже приведено два примера перенаправления.  
  
-   При создании узла службы конструктор получает управление от вызывающего кода, или вызывающий код выполняет перенаправление на конструктор.  По завершении выполнения конструктор возвращает управление вызывающему коду, или конструктор выполняет перенаправление обратно на вызывающий код.  Это случай отношения вложенности.  
  
-   Когда прослушиватель начинает обрабатывать данные транспорта, он создает новый поток и передает действию Receive Bytes соответствующий контекст для обработки, т. е. передает управление и данные.  По завершении обработки запроса этим потоком действие Receive Bytes ничего не передает обратно прослушивателю.  В этом случае имеет место перенаправление на новое действие потока, однако перенаправления от действия потока не происходит.  Два действия связаны, но не являются вложенными.  
  
## Последовательность перенаправления между действиями  
 Корректная последовательность перенаправления между действиями включает следующие шаги.  
  
1.  Начало нового действия \(заключается в выборе нового идентификатора gAId\).  
  
2.  Выдача трассировки перенаправления на этот новый идентификатор gAId от текущего идентификатора действия.  
  
3.  Задание нового идентификатора в локальной памяти потока.  
  
4.  Выдача трассировки Start, обозначающей начало нового действия.  
  
5.  Возврат к исходному действию заключается в следующем:  
  
6.  выдача трассировки перенаправления к исходному идентификатору gAId;  
  
7.  выдача трассировки Stop, обозначающей конец нового действия;  
  
8.  присвоение локальной памяти потока старого идентификатора gAId.  
  
 В следующем примере кода показано, как это сделать.  В этом примере предполагается, что при перенаправлении на новое действие совершается блокирующий вызов, и приводятся трассировки приостановки\/возобновления.  
  
```  
// 0. Create a trace source  
TraceSource ts = new TraceSource(“myTS”);  
// 1. remember existing (“ambient”) activity for clean up  
Guid oldGuid = Trace.CorrelationManager.ActivityId;  
// this will be our new activity  
Guid newGuid = Guid.NewGuid();   
// 2. call transfer, indicating that we are switching to the new AID  
ts.TraceTransfer(667, "Transferring.", newGuid);  
// 3. Suspend the current activity.  
ts.TraceEvent(TraceEventType.Suspend, 667, "Suspend: Activity " + i-1);  
// 4. set the new AID in TLS  
Trace.CorrelationManager.ActivityId = newGuid;  
// 5. Emit the start trace  
ts.TraceEvent(TraceEventType.Start, 667, "Boundary: Activity " + i);  
// trace something  
ts.TraceEvent(TraceEventType.Information, 667, "Hello from activity " + i);  
// Perform Work  
// some work.  
// Return  
ts.TraceEvent(TraceEventType.Information, 667, "Work complete on activity " + i);   
// 6. Emit the transfer returning to the original activity  
ts.TraceTransfer(667, "Transferring Back.", oldGuid);  
// 7. Emit the End trace  
ts.TraceEvent(TraceEventType.Stop, 667, "Boundary: Activity " + i);  
// 8. Change the tls variable to the original AID  
Trace.CorrelationManager.ActivityId = oldGuid;    
// 9. Resume the old activity  
ts.TraceEvent(TraceEventType.Resume, 667, "Resume: Activity " + i-1);  
```  
  
## См. также  
 [Настройка трассировки](../../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md)   
 [Использование программы Service Trace Viewer для просмотра скоррелированных трассировок и устранения неполадок](../../../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)   
 [Сценарии сквозной трассировки](../../../../../docs/framework/wcf/diagnostics/tracing/end-to-end-tracing-scenarios.md)   
 [Программа Service Trace Viewer \(SvcTraceViewer.exe\)](../../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)