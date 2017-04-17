---
title: "&lt;workflowIdle&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: b2ef703c-3e01-4213-9d2e-c14c7dba94d2
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;workflowIdle&gt;
Поведение службы, управляющее выгрузкой и сохранением простаивающих экземпляров рабочего процесса.  
  
## Синтаксис  
  
```  
  
<behaviors>  
  <serviceBehaviors>  
    <behavior name=String">  
      <workflowIdle timeToPersist=”TimeSpan”  
          timeToUnload=”TimeSpan” />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
  
```  
  
## Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### Атрибуты  
  
|Атрибут|Описание|  
|-------------|--------------|  
|timeToPersist|Значение Timespan, указывающее интервал, который возникает между моментом, когда рабочий процесс становится неактивным, и его сохранением.  Значением по умолчанию является TimeSpan.MaxValue.<br /><br /> Начало интервала определяется моментом, когда экземпляр рабочего процесса становится неактивным.  Этот атрибут может оказаться полезным в том случае, если необходимо более интенсивно сохранять экземпляр рабочего процесса, оставляя его в памяти как можно дольше.  Этот атрибут допустим только в том случае, если его значение меньше атрибута **timeToUnload**.  Если значение больше, оно не учитывается.  Если время, указанное в атрибуте, истекло раньше значения, определенного атрибутом **timeToUnload**, то сохранение должно быть завершено до того, как рабочий процесс будет выгружен.  Это означает, что операция выгрузки может быть задержана, пока рабочий процесс не будет сохранен.  Уровень сохраняемости ответственен за обработку повторений для временных ошибок и выдает исключения только для неустранимых ошибок.  В связи с этим все исключения, возникшие во время сохранения, считаются неустранимыми, и производится прерывание работы экземпляра рабочего процесса.|  
|timeToUnload|Значение Timespan, указывающее интервал времени от момента, когда рабочий процесс стал неактивным, до его выгрузки.  Значение по умолчанию \- 1 минута.<br /><br /> При выгрузке рабочего процесса подразумевается, что было произведено его сохранение.  Если этот атрибут имеет нулевое значение, экземпляр рабочего процесса сохраняется и выгружается сразу после того, как становится неактивным.  Если задать этому атрибуту значение TimeSpan.MaxValue, операция выгрузки будет фактически отключена.  Простаивающие экземпляры рабочего процесса не выгружаются.|  
  
### Дочерние элементы  
 Отсутствует.  
  
### Родительские элементы  
  
|Элемент|Описание|  
|-------------|--------------|  
|[\<behavior\> для \<serviceBehaviors\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/behavior-of-servicebehaviors-of-workflow.md)|Указывает элемент поведения.|  
  
## См. также  
 <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior>   
 <xref:System.ServiceModel.Activities.Configuration.WorkflowIdleElement>