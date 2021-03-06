---
title: "Несколько контрактов"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2bef319b-fe9c-4d49-ac6c-dfb23eb35099
caps.latest.revision: "14"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: bfd9446edc176e3d4cb014db578990971128707c
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="multiple-contracts"></a>Несколько контрактов
В образце нескольких контрактов показано, как реализовать для службы более одного контракта и как настроить конечные точки для взаимодействия с каждым из реализованных контрактов. Этот пример построен на [Приступая к работе](../../../../docs/framework/wcf/samples/getting-started-sample.md). Служба была изменена, чтобы в ней было определено два контракта - контракт `ICalculator` и контракт `ICalculatorSession`.  
  
> [!NOTE]
>  Процедура настройки и инструкции по построению для данного образца приведены в конце этого раздела.  
  
 Класс службы реализует контракты `ICalculator` и `ICalculatorSession`. Поскольку одному из контрактов требуется сеанс, служба использует режим экземпляра <xref:System.ServiceModel.InstanceContextMode.PerSession> для поддержки состояния в течение времени существования сеанса.  
  
 Конфигурация службы была изменена, чтобы в ней определялось две конечных точки для обоих контрактов. Конечная `ICalculator` точка доступна по базовому адресу с использованием привязки `basicHttpBinding`. Конечная точка `ICalculatorSession` доступна по адресу "базовый_адрес/сеанс" с использованием привязки `wsHttpBinding`, атрибут `bindingConfiguration` которой имеет значение `BindingWithSession`, как показано в следующем образце конфигурации.  
  
```xml  
<service   
    name="Microsoft.ServiceModel.Samples.CalculatorService"  
    behaviorConfiguration="CalculatorServiceBehavior">  
  <!-- ICalculator endpoint is exposed using BasicBinding at the base  
       address provided by host:   
       http://localhost/servicemodelsamples/service.svc  -->  
  <endpoint address=""  
            binding="basicHttpBinding"  
            contract="Microsoft.ServiceModel.Samples.ICalculator" />  
  <!-- ICalculatorSession endpoint is exposed using BindingWithSession  
       at {baseaddress}/session:  
       http://localhost/servicemodelsamples/service.svc/session -->  
  <endpoint address="session"  
            binding="wsHttpBinding"  
            bindingConfiguration="BindingWithSession"   
           contract="Microsoft.ServiceModel.Samples.ICalculatorSession" />  
  ...  
</service>  
```  
  
 Теперь созданный код клиента содержит клиентский класс как для исходного контракта `ICalculator`, так и для нового контракта `ICalculatorSession`. Конфигурация и код клиента были изменены, чтобы он мог взаимодействовать с каждым из контрактов через соответствующую конечную точку службы.  
  
 Клиент является консольным приложением Windows (EXE). Служба размещается в службах IIS.  
  
 В окне консольного приложения клиента отображаются операции, передаваемые в каждую из конечных точек, сначала для базовой конечной точки, а затем для защищенной конечной точки.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Настройка, сборка и выполнение образца  
  
1.  Убедитесь, что вы выполнили [выполняемая однократно процедура настройки для образцов Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Чтобы создать выпуск решения на языке C# или Visual Basic .NET, следуйте инструкциям в разделе [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Для запуска образца в конфигурации одного или нескольких компьютерах, следуйте инструкциям в [выполнение образцов Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере. Перед продолжением проверьте следующий каталог (по умолчанию).  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите на страницу [Примеры Windows Communication Foundation (WCF) и Windows Workflow Foundation (WF) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) , чтобы скачать все примеры [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] и [!INCLUDE[wf1](../../../../includes/wf1-md.md)] . Этот образец расположен в следующем каталоге.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\MultipleContracts`  
  
## <a name="see-also"></a>См. также
