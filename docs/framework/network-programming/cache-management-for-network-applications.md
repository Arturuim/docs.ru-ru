---
title: "Управление кэшем для сетевых приложений | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "кэш [платформа .NET Framework], сетевые приложения"
  - "сетевые ресурсы, кэширование"
  - "Интернет, кэширование"
ms.assetid: fc258a40-f370-434f-ae09-4a8cb11ddaeb
caps.latest.revision: 13
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# Управление кэшем для сетевых приложений
В этом разделе и связанные с ним в подразделах описываются кэшировать для ресурсов, полученных с помощью <xref:System.Net.WebClient>, <xref:System.Net.WebRequest>, <xref:System.Net.HttpWebRequest> и классы <xref:System.Net.FtpWebRequest>.  
  
 Кэш предоставляет временное хранилище для ресурсов, запрошенных приложением.  Если приложение запрашивает один и тот же ресурс более одного раза, ресурс может быть возвращен из кэша, избежать издержек re\- запрос его от сервера.  Кэширование позволяет повысить производительность приложения путем уменьшения времени, необходимого для получил запрошенного ресурса.  Кэширование может сократить сетевой трафик путем сокращения количества отключений к серверу.  Пока кэширование улучшает производительность, она увеличивает риск, ресурс, возвращаемый в приложение несвеж, означать, что он не идентичен ресурсу, который будет отправлять сервером, если не была прячущ в кэше.  
  
 Кэширование может разрешить неавторизованные пользователи или процессы для считывания конфиденциальные данные.  Проверенный ответ, который находится в кэше может быть извлечен из кэша без дополнительной авторизации.  Если кэширование включено, то измените в <xref:System.Net.WebRequest.CachePolicy%2A> к <xref:System.Net.Cache.RequestCacheLevel> или <xref:System.Net.Cache.RequestCacheLevel> для отключения кэширования для этого запроса.  
  
 Из\-за вопросы безопасности, кэширование **not** рекомендованное в сценариях среднего уровня.  
  
## В этом подразделе  
 [Политика кэша](../../../docs/framework/network-programming/cache-policy.md)  
 Объясняет, что политика кэша, и, как определить одно.  
  
 [Политики кэша на основе расположения](../../../docs/framework/network-programming/location-based-cache-policies.md)  
 Определяет каждый тип места хранения\- доступных ресурсов на основе политики кэша HTTP\-протокола \(HTTP и HTTPs\).  
  
 [Политики кэша на основе времени](../../../docs/framework/network-programming/time-based-cache-policies.md)  
 Описывает условие, которое можно использовать для настройки Time\- на основе политики кэша.  
  
 [Настройка кэширования в сетевых приложениях](../../../docs/framework/network-programming/configuring-caching-in-network-applications.md)  
 Описывается программное создание политики кэша и запрашивает, что кэширование использования.  
  
## Ссылка  
 <xref:System.Net.Cache>  
 Определяет типы и перечисления, используемые для определения политики кэша для ресурсов, полученных с помощью <xref:System.Net.WebRequest>, <xref:System.Net.HttpWebRequest> и классы <xref:System.Net.FtpWebRequest>.