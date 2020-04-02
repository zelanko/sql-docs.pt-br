---
title: Inicializando objetos de assembly personalizados | Microsoft Docs
ms.date: 03/03/2017
description: Saiba como inicializar classes personalizadas com os valores disponibilizados pelas coleções de objetos globais do relatório.
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.topic: reference
helpviewer_keywords:
- initializing custom assemblies [Reporting Services]
- custom assemblies [Reporting Services], initializing
- OnInit method
ms.assetid: 26fd74dc-d02f-40f7-aeb3-50ce05e9e6b9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c2f0f85904b4541ed478664f5f39e19cc309cf9a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "80217025"
---
# <a name="initializing-custom-assembly-objects"></a>Inicializando objetos assembly personalizados
  Em alguns casos, talvez você precise inicializar valores de propriedade e de campo em suas classes assembly personalizadas ao instanciá-las. É mais provável que você tenha de inicializar as suas classes personalizadas com valores disponíveis a partir de coleções de objetos globais do relatório. Faça isso substituindo o método **OnInit** do objeto **Code** de um relatório. Para acessar **OnInit**, use o elemento **Code** da definição de relatório. Há duas técnicas para inicializar valores de propriedade ou de campo das classes em um assembly personalizado que você planeja usar em seu relatório: Você pode declarar e criar uma instância de sua classe usando **OnInit** ou pode chamar um método publicamente disponível usando **OnInit**.  
  
## <a name="global-object-collections-and-initialization"></a>Coleções e inicialização de objetos globais  
 Várias coleções estão disponíveis para que você inicialize suas variáveis de classe personalizadas. Use as coleções **Globals** e **User**. As coleções **Parameters**, **Fields** e **ReportItems** não estão disponíveis no ponto do ciclo de vida do relatório quando o método **OnInit** é invocado. Para usar as coleções compartilhadas, **Globals** ou **User**, você precisa incluir a referência de objeto **Report**. Por exemplo, para inicializar a classe personalizada com base no idioma atual do usuário que está acessando o relatório, o elemento **Code** poderá ter esta aparência:  
  
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
  
 Outra forma de inicializar os valores de propriedade e de campo das classes em assemblies personalizados é chamar um método disponível publicamente definido com base no método **OnInit**. Primeiro, você precisa adicionar um nome de instância para a sua classe ao arquivo de definição de relatório. Depois de adicionar a referência de assembly apropriada e o nome de instância, você poderá chamar o seu método de inicialização para inicializar valores de propriedade e de campo para a sua classe. O método **OnInit** poderá ser parecido com o seguinte:  
  
```  
<Code>  
   Protected Overrides Sub OnInit()  
      m_myClass.MyInitializationMethod(Report.User!Language, _  
         Report.Globals!ExecutionTime)  
   End Sub  
</Code>  
```  
  
 Para obter mais informações sobre como adicionar um nome de instância e uma referência de assembly à classe personalizada, consulte [Adicionar uma referência de assembly a um relatório &#40;SSRS&#41;](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md).  
  
 Para obter mais informações sobre coleções de objetos globais, consulte [Coleções internas em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Usar assemblies personalizados com relatórios](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
