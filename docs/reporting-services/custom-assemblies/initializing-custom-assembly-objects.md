---
title: Inicializando objetos Assembly personalizados | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- initializing custom assemblies [Reporting Services]
- custom assemblies [Reporting Services], initializing
- OnInit method
ms.assetid: 26fd74dc-d02f-40f7-aeb3-50ce05e9e6b9
caps.latest.revision: 36
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: dd3f6682e6297f86fbc4e67b98f5df48c7e94281
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="initializing-custom-assembly-objects"></a>Inicializando objetos assembly personalizados
  Em alguns casos, talvez você precise inicializar valores de propriedade e de campo em suas classes assembly personalizadas ao instanciá-las. É mais provável que você tenha de inicializar as suas classes personalizadas com valores disponíveis a partir de coleções de objetos globais do relatório. Para fazer isso, substituindo o **OnInit** método o **código** objeto de um relatório. Para acessar **OnInit**, use o **código** elemento da definição de relatório. Existem duas técnicas para inicializar valores de propriedade ou campo das classes em um assembly personalizado que você planeja usar em seu relatório: você pode declarar e criar uma nova instância da sua classe usando **OnInit**, ou você pode chamar um método disponível publicamente usando **OnInit**.  
  
## <a name="global-object-collections-and-initialization"></a>Coleções e inicialização de objetos globais  
 Várias coleções estão disponíveis para que você inicialize suas variáveis de classe personalizadas. Você pode usar o **globais** e **usuário** coleções. O **parâmetros**, **campos** e **ReportItems** coleções não estão disponíveis para você no ponto do ciclo de vida do relatório quando o **OnInit** método é invocado. Para usar as coleções compartilhadas, **globais** ou **usuário**, você precisa incluir o **relatório** referência de objeto. Por exemplo, para inicializar sua classe personalizada com base no idioma atual do usuário que está acessando o relatório, seu **código** elemento pode parecer com o seguinte:  
  
```  
<Code>  
   Dim m_myClass As MyClass  
  
   Protected Overrides Sub OnInit()  
      m_myClass = new MyClass(Report.User!Language, _  
         Report.Globals!ExecutionTime)  
   End Sub  
</Code>  
```  
  
 Uma forma de inicializar os valores de propriedade e de campo de uma classe como mostrado anteriormente é declarar a sua classe e criar uma nova instância dela chamando um construtor substituído.  
  
 Outra maneira de inicializar os valores de propriedade e o campo das classes em seus assemblies personalizados é chamar um método disponível publicamente definido a partir de **OnInit** método. Primeiro, você precisa adicionar um nome de instância para a sua classe ao arquivo de definição de relatório. Depois de adicionar a referência de assembly apropriada e o nome de instância, você poderá chamar o seu método de inicialização para inicializar valores de propriedade e de campo para a sua classe. O **OnInit** método pode parecer com o seguinte:  
  
```  
<Code>  
   Protected Overrides Sub OnInit()  
      m_myClass.MyInitializationMethod(Report.User!Language, _  
         Report.Globals!ExecutionTime)  
   End Sub  
</Code>  
```  
  
 Para obter mais informações sobre como adicionar um nome de instância e de referência de assembly para sua classe personalizada, consulte [adicionar uma referência de Assembly para um relatório &#40; SSRS &#41; ](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md).  
  
 Para obter mais informações sobre as coleções de objetos globais, consulte [coleções internas em expressões &#40; Construtor de relatórios e SSRS &#41; ](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
## <a name="see-also"></a>Consulte também  
 [Usando assemblies personalizados com relatórios](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
