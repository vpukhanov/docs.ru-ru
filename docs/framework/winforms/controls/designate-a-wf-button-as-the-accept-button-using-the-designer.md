---
title: "Практическое руководство. Создание кнопки принятия в формах Windows Forms с помощью конструктора"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- buttons [Windows Forms], default on Windows Forms
- Accept button on Windows Forms
- Button control [Windows Forms], designating as default
- Windows Forms controls, default button on form
ms.assetid: a1da0590-755f-49f2-aca7-609fac6351bf
caps.latest.revision: "13"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: be2fe788be4aeaa2e8eccaaf539a08b076f2da01
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-designate-a-windows-forms-button-as-the-accept-button-using-the-designer"></a>Практическое руководство. Создание кнопки принятия в формах Windows Forms с помощью конструктора
В любой форме Windows Forms можно назначить <xref:System.Windows.Forms.Button> отображения элемента управления «принять», также известные как кнопка по умолчанию. Каждый раз, когда пользователь нажимает клавишу ВВОД, нажатии кнопки по умолчанию независимо от других элементов управления в форме имеет фокус. Исключение составляют при другой кнопки элемента управления с фокусом — в этом случае будет нажата кнопка с фокусом, многострочное текстовое поле, или пользовательский элемент управления, который перехватывает клавишу ВВОД.  
  
> [!NOTE]
>  Отображаемые диалоговые окна и команды меню могут отличаться от описанных в справке в зависимости от текущих параметров или выпуска. Чтобы изменить параметры, выберите в меню **Сервис** пункт **Импорт и экспорт параметров** . Дополнительные сведения см. в статье [Настройка параметров разработки в Visual Studio](http://msdn.microsoft.com/library/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### <a name="to-designate-the-accept-button"></a>Чтобы создать кнопку «принять»  
  
1.  Выберите форму, в которой находится кнопка.  
  
2.  В **свойства** задайте формы <xref:System.Windows.Forms.Form.AcceptButton%2A> свойства <xref:System.Windows.Forms.Button> имя элемента управления.  
  
## <a name="see-also"></a>См. также  
 <xref:System.Windows.Forms.Form.AcceptButton%2A>  
 [Общие сведения об элементе управления Button](../../../../docs/framework/winforms/controls/button-control-overview-windows-forms.md)  
 [Способы активации элемента управления Button в Windows Forms](../../../../docs/framework/winforms/controls/ways-to-select-a-windows-forms-button-control.md)  
 [Практическое руководство. Обработка события нажатия кнопки в Windows Forms](../../../../docs/framework/winforms/controls/how-to-respond-to-windows-forms-button-clicks.md)  
 [Практическое руководство. Создание кнопки отмены в формах Windows Forms с помощью конструктора](../../../../docs/framework/winforms/controls/designate-a-wf-button-as-the-cancel-button-using-the-designer.md)  
 [Элемент управления Button](../../../../docs/framework/winforms/controls/button-control-windows-forms.md)
