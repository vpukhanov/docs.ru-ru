---
title: Объект My.WebServices
ms.date: 07/20/2015
ms.prod: .net
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- My.WebServices
- My.MyProject.WebServices
helpviewer_keywords:
- My.WebServices object
ms.assetid: f188dc05-2c75-41b6-bb68-122d1c3110a2
caps.latest.revision: 17
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: a9f2c4017a1df8059f2cc57e7c30a96c474cfda0
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="mywebservices-object"></a>Объект My.WebServices
Предоставляет свойства для создания и доступа к один экземпляр каждого веб-службы XML ссылается текущий проект.  
  
## <a name="remarks"></a>Примечания  
 Объект `My.WebServices` предоставляет экземпляр каждой веб-службы, на которую ссылается текущий проект. Каждый экземпляр создается по запросу. Доступ к этим веб-службам можно получить через свойства объекта `My.WebServices`. Имя свойства совпадает с именем веб-службы, к которой обращается свойство. Любой класс, наследуемый от <xref:System.Web.Services.Protocols.SoapHttpClientProtocol>, является веб-службой. Сведения о добавлении веб-служб в проект см. в разделе [доступ к веб-службам приложения](../../../visual-basic/developing-apps/programming/accessing-application-web-services.md).  
  
 `My.WebServices` Объект предоставляет только веб-службы, связанный с текущим проектом. Он не предоставляет доступ к веб-службам, объявленным в присоединенных DLL. Для доступа к веб-службу, которая предоставляет библиотеку DLL, необходимо использовать полное имя веб-службы в виде *DllName*. *ИмяВебСлужбы*. Дополнительные сведения см. в разделе [доступ к веб-службам приложения](../../../visual-basic/developing-apps/programming/accessing-application-web-services.md).  
  
 Объект и его свойства недоступны для веб-приложений.  
  
## <a name="properties"></a>Свойства  
 Каждое свойство `My.WebServices` объект предоставляет доступ к экземпляру веб-службы, на которые имеются ссылки в текущем проекте. Имя свойства совпадает с именем веб-службы, который обращается к свойству, а тип свойства совпадает с типом веб-службы.  
  
> [!NOTE]
>  Если имеется конфликт имен, имя свойства для доступа к веб-службы является *RootNamespace*_*имен*\_*ServiceName*. Например, рассмотрим две веб-службы с именем `Service1`. Если один из этих служб находится в корневом пространстве имен `WindowsApplication1` и в пространстве имен `Namespace1`, доступ к этой службе с помощью `My.WebServices.WindowsApplication1_Namespace1_Service1`.  
  
 При первом обращении к одной из `My.WebServices` свойств объекта, он создает новый экземпляр веб-службы и сохраняет его. Последующие обращения к этим свойствам возвращают этот экземпляр веб-службы.  
  
 Веб-службы можно освободить путем назначения `Nothing` свойства для этой веб-службы. Метод задания свойства назначает `Nothing` с сохраненным значением. Если присвоить любое значение, отличное от `Nothing` к свойству, методу задания создает исключение <xref:System.ArgumentException> исключение.  
  
 Можно проверить, является ли свойство `My.WebServices` объект сохраняет экземпляр веб-службы с помощью `Is` или `IsNot` оператор. Эти операторы можно использовать для проверки, если значение свойства `Nothing`.  
  
> [!NOTE]
>  Как правило `Is` или `IsNot` оператор имеет считывается значение свойства для выполнения сравнения. Тем не менее если в настоящее время хранит свойство `Nothing`, свойство создает новый экземпляр веб-службы и затем возвращает этот экземпляр. Однако компилятор Visual Basic обрабатывает свойства `My.WebServices` специально объекта и позволяет `Is` или `IsNot` проверить состояние свойства без изменения его значения.  
  
## <a name="example"></a>Пример  
 В этом примере вызывается `FahrenheitToCelsius` метод `TemperatureConverter` веб-службы XML и возвращает результат.  
  
 [!code-vb[VbVbalrMyWebService#1](../../../visual-basic/language-reference/objects/codesnippet/VisualBasic/my-webservices-object_1.vb)]  
  
 Для работы этого примера проект должен ссылаться на веб-службы с именем `Converter`, и должен предоставлять эту веб-службу `ConvertTemperature` метод. Дополнительные сведения см. в разделе [доступ к веб-службам приложения](../../../visual-basic/developing-apps/programming/accessing-application-web-services.md).  
  
 Этот код не работает в проект веб-приложения.  
  
## <a name="requirements"></a>Требования  
  
### <a name="availability-by-project-type"></a>Доступность по типу проекта  
  
|Тип проекта|Доступно|  
|---|---|  
|Приложение Windows|**Да**|  
|Библиотека классов|**Да**|  
|Консольное приложение|**Да**|  
|Библиотека элементов управления Windows|**Да**|  
|Библиотека веб-элементов управления|**Да**|  
|Служба Windows|**Да**|  
|Веб-сайт|Нет|  
  
## <a name="see-also"></a>См. также  
 <xref:System.Web.Services.Protocols.SoapHttpClientProtocol>  
 <xref:System.ArgumentException>  
 [Доступ к веб-службам приложения](../../../visual-basic/developing-apps/programming/accessing-application-web-services.md)
