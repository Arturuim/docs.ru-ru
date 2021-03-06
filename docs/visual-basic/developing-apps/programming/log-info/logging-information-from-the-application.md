---
title: "Запись сведений в журнал из приложения (Visual Basic)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Log object
- My.Log object
- applications [Visual Basic], logging information from
- logging
- My.Application.Log object
- examples [Visual Basic], logging application information
ms.assetid: 8bf4f047-22d6-48d6-aec5-93b98ad5b8e8
caps.latest.revision: 12
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 58f21df20425b0164586143ad5af6f363a90c3ef
ms.contentlocale: ru-ru
ms.lasthandoff: 07/28/2017

---
# <a name="logging-information-from-the-application-visual-basic"></a>Запись сведений в журнал из приложения (Visual Basic)
Этот раздел содержит сведения о том, как регистрировать в журнале информацию из приложения с помощью объектов `My.Application.Log` или `My.Log` и как расширить возможности ведения журнала в приложении.  
  
 Объект `Log` предоставляет методы для записи информации в прослушиватели журнала приложения, а свойство `TraceSource` объекта `Log` предоставляет подробные сведения о конфигурации. Объект `Log` настраивается в файле конфигурации приложения.  
  
 Объект `My.Log` доступен только для приложений ASP.NET. Для клиентских приложений следует использовать объект `My.Application.Log`. Для получения дополнительной информации см. <xref:Microsoft.VisualBasic.Logging.Log>.  
  
## <a name="tasks"></a>Задачи  
  
|Целевой тип|См.|  
|--------|---------|  
|Запись информации о событиях в журналы приложения.|[Практическое руководство. Запись сообщений в журнал](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-log-messages.md)|  
|Запись информации об исключениях в журналы приложения.|[Практическое руководство. Запись в журнал сведений об исключениях](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)|  
|Запись данных трассировки в журналы приложения во время запуска и завершения работы приложения.|[Практическое руководство. Запись в журнал сообщений при запуске и завершении приложения](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-messages-when-the-application-starts-or-shuts-down.md)|  
|Настройка объекта `My.Application.Log` для записи информации в текстовый файл.|[Практическое руководство. Запись сведений о событиях в текстовый файл](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-event-information-to-a-text-file.md)|  
|Настройка объекта `My.Application.Log` для записи информации в журнал событий.|[Практическое руководство. Запись в журнал событий приложения](../../../../visual-basic/developing-apps/programming/log-info/how-to-write-to-an-application-event-log.md)|  
|Изменение места, в которое объект `My.Application.Log` записывает информацию.|[Пошаговое руководство. Изменение места записи сведений для My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)|  
|Выбор места, в которое объект `My.Application.Log` записывает информацию.|[Пошаговое руководство. Определение места записи сведений для My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)|  
|Создание пользовательского прослушивателя журнала для `My.Application.Log`.|[Пошаговое руководство. Создание пользовательских прослушивателей журнала](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-creating-custom-log-listeners.md)|  
|Фильтрация выходных данных журналов `My.Application.Log`.|[Пошаговое руководство. Фильтрация вывода My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-filtering-my-application-log-output.md)|  
  
## <a name="see-also"></a>См. также  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 [Работа с журналами приложения](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)   
 [Устранение неполадок, связанных с прослушивателями журнала](../../../../visual-basic/developing-apps/programming/log-info/troubleshooting-log-listeners.md)

