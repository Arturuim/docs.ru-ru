---
title: "Конечные точки SOAP и HTTP | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e3c8be75-9dda-4afa-89b6-a82cb3b73cf8
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Конечные точки SOAP и HTTP
Данный образец демонстрирует реализацию службы на основе RPC и предоставление ее в формате протокола SOAP или формате "Plain Old XML" \(POX\) с помощью модели веб\-программирования [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  Дополнительные сведения о привязке HTTP для этой службы см. в образце [Базовая служба HTTP](../../../../docs/framework/wcf/samples/basic-http-service.md).  В данном образце акцент сделан на особенностях предоставления одной и той же службы через протокол SOAP и HTTP с использованием разных привязок.  
  
## Демонстрации  
 Предоставление службы RPC через протокол SOAP и HTTP с использованием [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Обсуждение  
 Данный образец состоит из двух компонентов: проекта веб\-приложения \(служба\), который содержит службу [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], и консольного приложения \(клиент\), которое вызывает операции службы с использованием привязок протокола SOAP и HTTP.  
  
 Служба [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] предоставляет 2 операции \- `GetData` и `PutData`, которые повторяют строку, переданную им на входе.  Операции службы помечены атрибутами <xref:System.ServiceModel.Web.WebGetAttribute> и <xref:System.ServiceModel.Web.WebInvokeAttribute>.  Эти атрибуты управляют HTTP\-проекцией операций.  Кроме того, они помечены атрибутом <xref:System.ServiceModel.OperationContractAttribute>, который позволяет предоставлять их через привязки протокола SOAP.  Метод службы `PutData` вызывает исключение <xref:System.ServiceModel.Web.WebFaultException>, которое отправляется обратно через HTTP с использованием кода состояния HTTP, а через SOAP как ошибка SOAP.  
  
 Файл Web.config конфигурирует для службы [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] следующие 3 конечные точки.  
  
-   Конечная точка ~\/service.svc\/mex предоставляет доступ к метаданным службы клиентам на основе SOAP.  
  
-   Конечная точка ~\/service.svc\/http позволяет клиентам получать доступ к службе с использованием привязки HTTP.  
  
-   Конечная точка ~\/service.svc\/soap позволяет клиентам получать доступ к службе с использованием привязки протокола SOAP.  
  
 Конечная точка HTTP настроена как стандартная конечная точка \<`webHttp`\> с атрибутом `helpEnabled`, имеющим значение `true`.  В результате этого служба предоставляет справочную страницу на основе XHTML по адресу ~\/service.svc\/http\/help, которую клиенты на основе HTTP могут использовать для доступа к службе.  
  
 Клиентский проект демонстрирует доступ к службе с использованием прокси протокола SOAP \(сформированного с помощью команды **Добавить ссылку на службу**\) и доступ к службе с использованием клиента <xref:System.Net.WebClient>.  
  
 Образец состоит из службы, размещенной на веб\-сервере, и консольного приложения.  Во время выполнения консольного приложения клиент совершает запросы к службе и выводит в окно консоли нужные сведения из ответов.  
  
#### Выполнение образца  
  
1.  Откройте решение для образца «SOAP and HTTP Endpoints».  
  
2.  Чтобы построить решение, нажмите CTRL\+SHIFT\+B.  
  
3.  Если окно **Обозреватель решений** не открыто, нажмите клавиши CTRL\+W, S, чтобы открыть его.  
  
4.  В окне **Обозреватель решений** щелкните правой кнопкой мыши проект **Service** и поместите курсор над пунктом контекстного меню **Отладка**, чтобы отобразить контекстное меню **Запустить новый экземпляр**.  Нажмите кнопку **Запустить новый экземпляр**.  Запускается сервер разработки ASP.NET, на котором размещается служба.  
  
5.  В окне обозревателя решений щелкните правой кнопкой мыши проект Client и поместите курсор над пунктом контекстного меню **Отладка**, чтобы отобразить контекстное меню **Запустить новый экземпляр**.  Нажмите кнопку **Запустить новый экземпляр**.  
  
6.  На клиенте открывается окно консоли с URI запущенной службы и URI HTML\-страницы справки для запущенной службы.  HTML\-страницу справки можно просмотреть в любой момент времени, введя URI этой страницы в браузере.  
  
7.  Во время работы образца клиент записывает состояние текущего действия.  
  
8.  Чтобы завершить клиентское консольное приложение, нажмите любую клавишу.  
  
9. Чтобы прекратить отладку службы, нажмите клавиши SHIFT\+F5.  
  
10. В области уведомлений Windows щелкните правой кнопкой мыши значок сервера разработчика ASP.NET и выберите в контекстном меню пункт **Остановить**.  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере.  Перед продолжением проверьте следующий каталог \(по умолчанию\).  
>   
>  `<диск_установки>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите на страницу [Образцы Windows Communication Foundation \(WCF\) и Windows Workflow Foundation \(WF\) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780), чтобы загрузить все образцы [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] и [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Этот образец расположен в следующем каталоге.  
>   
>  `<диск_установки>:\WF_WCF_Samples\WCF\Basic\Web\SoapAndHttpEndpoints`