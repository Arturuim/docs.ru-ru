---
title: "Практическое руководство. Печать в Windows Forms с использованием предварительного просмотра | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "печать [Windows Forms], использование предварительного просмотра"
  - "печать, с предварительным просмотром"
  - "предварительный просмотр"
ms.assetid: 4a16f7e2-ae10-4485-b0ae-3d558334d0fe
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Практическое руководство. Печать в Windows Forms с использованием предварительного просмотра
При программировании с использованием Windows Forms в качестве дополнения к службам печати часто предлагается возможность предварительного просмотра. Легким способом добавления предварительного просмотра в приложение является использование элемента управления <xref:System.Windows.Forms.PrintPreviewDialog> в сочетании с логикой обработки событий <xref:System.Drawing.Printing.PrintDocument.PrintPage> для печати файла.  
  
### Предварительный просмотр текстового документа с помощью элемента управления PrintPreviewDialog  
  
1.  Добавьте в форму элемент управления <xref:System.Windows.Forms.PrintPreviewDialog>, <xref:System.Drawing.Printing.PrintDocument> и две строки.  
  
     [!code-csharp[System.Drawing.Printing.PrintPreviewExample#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/CS/Form1.cs#1)]
     [!code-vb[System.Drawing.Printing.PrintPreviewExample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/VB/Form1.vb#1)]  
  
2.  Укажите в качестве значения свойства <xref:System.Drawing.Printing.PrintDocument.DocumentName%2A> документ, который нужно напечатать, а затем откройте документ и прочтите его содержимое в строку, добавленную ранее.  
  
     [!code-csharp[System.Drawing.Printing.PrintPreviewExample#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/CS/Form1.cs#2)]
     [!code-vb[System.Drawing.Printing.PrintPreviewExample#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/VB/Form1.vb#2)]  
  
3.  Как и при печати документа, для расчета числа строк на странице и отрисовки содержимого документа в обработчике событий <xref:System.Drawing.Printing.PrintDocument.PrintPage> используется свойство <xref:System.Drawing.Printing.PrintPageEventArgs.Graphics%2A> класса <xref:System.Drawing.Printing.PrintPageEventArgs> и содержимое файла. Нарисовав очередную страницу, проверьте, является ли она последней, и установите соответствующим образом свойство <xref:System.Drawing.Printing.PrintPageEventArgs.HasMorePages%2A> класса <xref:System.Drawing.Printing.PrintPageEventArgs>. Событие <xref:System.Drawing.Printing.PrintDocument.PrintPage> возникает до тех пор, пока значение свойства <xref:System.Drawing.Printing.PrintPageEventArgs.HasMorePages%2A> не станет равно `false`. После завершения отрисовки документа сбросьте строку, подлежащую отрисовке. Кроме того, убедитесь в том, что событие <xref:System.Drawing.Printing.PrintDocument.PrintPage> связано со своим методом обработки событий.  
  
    > [!NOTE]
    >  Если поддержка печати уже реализована в приложении, то, возможно, шаги 2 и 3 были выполнены ранее.  
  
     В примере кода ниже обработчик событий используется для печати файла testPage.txt тем шрифтом, который используется в форме.  
  
     [!code-csharp[System.Drawing.Printing.PrintPreviewExample#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/CS/Form1.cs#3)]
     [!code-vb[System.Drawing.Printing.PrintPreviewExample#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/VB/Form1.vb#3)]  
  
4.  Присвойте свойству <xref:System.Windows.Forms.PrintPreviewDialog.Document%2A> элемента управления <xref:System.Windows.Forms.PrintPreviewDialog> значение компонента <xref:System.Drawing.Printing.PrintDocument> в форме.  
  
     [!code-csharp[System.Drawing.Printing.PrintPreviewExample#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/CS/Form1.cs#5)]
     [!code-vb[System.Drawing.Printing.PrintPreviewExample#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/VB/Form1.vb#5)]  
  
5.  Вызовите метод <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> элемента управления <xref:System.Windows.Forms.PrintPreviewDialog>. Как правило, метод <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> вызывается из метода обработки событий <xref:System.Windows.Forms.Control.Click> кнопки. Вызов метода <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> приводит к возникновению события <xref:System.Drawing.Printing.PrintDocument.PrintPage> и отрисовке выходных данных в элементе управления <xref:System.Windows.Forms.PrintPreviewDialog>. Когда пользователь нажимает на значок печати в диалоговом окне, событие <xref:System.Drawing.Printing.PrintDocument.PrintPage> вызывается снова. При этом выходные данные отправляются на принтер, а не в диалоговое окно предварительного просмотра. Вот почему в шаге 3 в конце процесса отрисовки сбрасывалась строка.  
  
     В примере ниже показан метод обработки событий <xref:System.Windows.Forms.Control.Click> для кнопки в форме. Этот метод вызывает методы для чтения документа и вывода окна предварительного просмотра.  
  
     [!code-csharp[System.Drawing.Printing.PrintPreviewExample#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/CS/Form1.cs#4)]
     [!code-vb[System.Drawing.Printing.PrintPreviewExample#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/VB/Form1.vb#4)]  
  
## Пример  
 [!code-csharp[System.Drawing.Printing.PrintPreviewExample#0](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/CS/Form1.cs#0)]
 [!code-vb[System.Drawing.Printing.PrintPreviewExample#0](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/VB/Form1.vb#0)]  
  
## Компиляция кода  
 Для этого примера требуются:  
  
-   ссылки на сборки System, System.Windows.Forms и System.Drawing.  
  
-   Дополнительные сведения о выполнении сборки этого примера из командной строки для [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] или [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] см. в разделе [Построение из командной строки](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) или [Построение из командной строки с помощью csc.exe](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md). Чтобы выполнить сборку этого примера в [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)], можно также вставить код в новый проект.  См. также [Практическое руководство. Компиляция и выполнение откомпилированного примера кода формы Windows Forms с помощью Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## См. также  
 [How to: Print a Multi\-Page Text File in Windows Forms](../../../../docs/framework/winforms/advanced/how-to-print-a-multi-page-text-file-in-windows-forms.md)   
 [Windows Forms Print Support](../../../../docs/framework/winforms/advanced/windows-forms-print-support.md)   
 [More Secure Printing in Windows Forms](../../../../docs/framework/winforms/more-secure-printing-in-windows-forms.md)